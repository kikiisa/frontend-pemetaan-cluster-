<template>
  <div class="map">
    <div class="h-96" id="map"></div>
  </div>
</template>
<style scoped>
#map {
  border-radius: 10px;
}
</style>
<script setup>
import L from "leaflet/dist/leaflet.js";
import { onMounted } from "vue";


const fetchMap = async () => {
  const url = "http://localhost:5000/api/results";
  const response = await fetch(url);
  const data = await response.json();

  // Inisialisasi map
  const map = L.map("map").setView([0.9070359, 123.4257745], 9);

  // Tambahkan tile layer OpenStreetMap
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
  }).addTo(map);

  // Contoh marker statis (bisa dihapus jika tidak dibutuhkan)
  L.marker([0.8724071, 123.581636]).addTo(map);

  // Iterasi data dari API
  data.map((values) => {
    console.log(values);

    // Tentukan ikon berdasarkan kategori
    let iconUrl = "";

    if (values.klaster_banjir === "Tinggi") {
      iconUrl = "tinggi.png";
    } else if (values.klaster_banjir === "Sedang") {
      iconUrl = "sedang.png";
    } else if (values.klaster_banjir === "Rendah") {
      iconUrl = "rendah.png";
    } else {
      iconUrl = "default.png"; // fallback jika kategori tidak dikenal
    }

    // Buat ikon custom
    const customIcon = L.icon({
      iconUrl: iconUrl,
      iconSize: [32, 32],
      iconAnchor: [16, 32],
      popupAnchor: [0, -32],
    });
    
    // Tambahkan marker ke peta
    L.marker([values.latitude, values.longitude], { icon: customIcon })
      .addTo(map)
      
      .bindPopup(`<b>${values.desa}</b>`);

  });
};

onMounted(() => {
  fetchMap();
});
</script>
