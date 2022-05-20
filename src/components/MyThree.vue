<script setup>
  import * as THREE from 'three';
  import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
  // import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
  import { onMounted, watch, defineProps, reactive } from 'vue';

  const props = defineProps({
    root: {
      type: String,
      required: true
    },
    cameraOptions: {
      type: Object,
      default: () => ({
        fov: 45,
        near: 1,
        far: 100
      })
    },
    lightOptions: {
      type: Object,
      default: () => ({
        color: 0xffffff,
        intensity: 1
      })
    },
    objectOptions: {
      type: Object,
      default: () => ({
        position: {
          x: 0,
          y: 0,
          z: -3
        },
        rotation: {
          x: 0,
          y: 0,
          z: 0
        }
      })
    },
    gltfUrl: {
      type: String,
      required: true
    },
    rotate: {
      type: Object,
      default: () => ({
        x: false,
        y: false,
        z: false
      })
    }
  });

  let renderer = reactive(undefined);
  let container = reactive(undefined);
  let camera = reactive(undefined);
  let scene = reactive(undefined);
  let object = reactive(undefined);

  watch(() => props.objectOptions, (currentValue) => {
    object.rotation.y = currentValue.rotation.y;
  }, { deep: true });

  const createRenderer = () => {
    renderer = new THREE.WebGLRenderer();
    container.append(renderer.domElement);
    renderer.setSize(container.offsetWidth, container.offsetHeight);
    renderer.setClearColor(0xffffff, 0)
  };

  const createCamera = () => {
    const { fov, near, far } = props.cameraOptions;
    camera = new THREE.PerspectiveCamera(fov, container.offsetWidth / container.offsetHeight, near, far);
  };

  const createScene = () => {
    scene = new THREE.Scene();
  };

  const init = () => {
    createRenderer();
    createCamera();
    createScene();
    createObject();
    createLight();
    update();
  };

  const createObject = () => {
    const { position, rotation } = props.objectOptions;
    const loader = new GLTFLoader();
    loader.load(
      props.gltfUrl,
      gltf => {
        object = gltf.scene; scene.add(object);
        object.position.set(position.x, position.y, position.z);
        object.rotation.set(rotation.x, rotation.y, rotation.z);
        },
      () => {},
      error => {console.log(error)}
    )
  };

  const createLight = () => {
    const { color, intensity } = props.lightOptions;
    const light = new THREE.AmbientLight(color, intensity);
    scene.add(light);
  };

  const update = () => {
    requestAnimationFrame(update);
    renderer.render(scene, camera);

    const { rotate } = props;
    if (object?.rotation) {
      if(rotate.x) {
        object.rotation.x += 0.01
      }

      if(rotate.y) {
        object.rotation.y += 0.01
      }

      if(rotate.z) {
        object.rotation.z += 0.01
      }
    }
  };

  const onWindowResize = () => {
    camera.aspect = container.offsetWidth / container.offsetHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(container.offsetWidth, container.offsetHeight);
  };

  onMounted(() => {
    container = document.querySelector(props.root);
    addEventListener('resize', onWindowResize);
    if (container) {
      init();
    }
  });
</script>
