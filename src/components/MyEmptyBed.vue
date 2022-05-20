<script setup>
import MyThree from './MyThree.vue';
</script>

<template>
  <a target="_blank" href="https://hoff.ru/catalog/spalnya/krovati/?tip=derevyannye" class="my-bed">
    <span
        class="header"
        style="color: black"
    >
      <h1>Empty bed</h1>
    </span>

    <my-three
        root=".my-bed"
        gltfUrl="models/emptyBed/scene.gltf"
        :object-options="{ position: { x: 0, y: 0, z: - 35 }, rotation: { x: 0.5, y: 0, z: 0 } }"
        :light-options="{color: 0xffffff, intensity: 3 }"
        :rotate="{ x: true, y: false, z: false}"
    />
  </a>
</template>

<style>
.my-bed {
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
