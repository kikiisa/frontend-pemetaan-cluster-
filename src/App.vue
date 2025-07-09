<script setup lang="ts">
import NavbarComponents from "./components/NavbarComponents.vue";
import MapsComponents from "./components/MapsComponents.vue";
import ChartComponents from "./components/ChartComponents.vue";
</script>
<template>
  <main class="lg:w-3/4 mx-auto">
    <NavbarComponents />
    <div class="bg-base-200 m-3 p-3  rounded-3xl shadow-2xs">
      <MapsComponents />
    </div>
    <div class="card">
      <div class="card-body flex flex-col">
         <h1 class="text-xl font-bold">Keterangan</h1>
         <div class="image flex flex-row gap-2">
          <div class="group flex flex-row gap-2">
            <figure>
              <img src="../src/assets/tinggi.png" width="30" alt="" srcset="">
            </figure>
            <h1 class="font-bold mt-1">Sangat Rawan</h1>
          </div>
          <div class="group flex flex-row gap-2">
            <figure>
              <img src="../src/assets/sedang.png" width="30" alt="" srcset="">
            </figure>
            <h1 class="font-bold mt-1">Rawan</h1>
          </div>
          <div class="group flex flex-row gap-2">
            <figure>
              <img src="../src/assets/rendah.png" width="30" alt="" srcset="">
            </figure>
            <h1 class="font-bold mt-1">Tidak Rawan</h1>
          </div>
         </div>
      </div>
    </div>
    
  </main>
</template>
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
