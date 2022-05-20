<script setup>
  import MyThree from './MyThree.vue';
</script>

<template>
  <a class="my-sheets" target="_blank" href="https://hoff.ru/catalog/tovary_dlya_doma/tekstil/" style="color: black">
    <span
      class="header"
    >
      <h1>Bedding</h1>
    </span>

    <my-three
      root=".my-sheets"
      gltfUrl="models/sheets/scene.gltf"
      :object-options="{ position: { x: 0, y: 0, z: - 5 }, rotation: { x: 0.5, y: 0, z: 0 } }"
      :light-options="{color: 0xffffff, intensity: 1.5 }"
      :rotate="{ x: false, y: true, z: false}"
    />
  </a>
</template>

<style>
  .my-sheets {
    width: 100%;
    height: 100vh;
    position: relative;
  }

  .header {
    position: absolute;
    top: 80%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-decoration: none;
  }
</style>
