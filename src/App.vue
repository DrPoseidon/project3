<script setup>
  import MySheets from "@/components/MySheets";
  import MyEmptyBed from "@/components/MyEmptyBed";
  import MyBed from "@/components/MyBed";
</script>

<template>
  <div class="app">
    <my-sheets class="object"/>
    <my-empty-bed class="object"/>
    <my-bed class="object"/>
  </div>
</template>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
  }

  .app {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
  }
</style>
