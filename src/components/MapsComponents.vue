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
  const map = L.map("map").setView([0.9070359, 123.4257745], 12);

  // Tambahkan tile layer OpenStreetMap
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
  }).addTo(map);

  // Contoh marker statis (bisa dihapus jika tidak dibutuhkan)
  

  // Iterasi data dari API
  data.map((values) => {
    console.log(values);

    // Tentukan ikon berdasarkan kategori
    let iconUrl = "";
    let circleColor = "";

    if (values.claster === "Sangat Rawan") {
    iconUrl = "tinggi.png";
    circleColor = "#ff0000"; // merah
  } else if (values.claster === "Rawan") {
    iconUrl = "sedang.png";
    circleColor = "#ffc107"; // kuning
  } else if (values.claster === "Tidak Rawan") {
    iconUrl = "rendah.png";
    circleColor = "#28a745"; // hijau
  } else {
    iconUrl = "default.png";
    circleColor = "#999"; // abu-abu default
  }
    // Buat ikon custom
    const customIcon = L.icon({
      iconUrl: iconUrl,
      iconSize: [32, 32],
      iconAnchor: [16, 32],
      popupAnchor: [0, -32],
    });
    let latlng = [values.lat, values.lng];
    // Tambahkan marker ke peta
    L.marker([values.lat, values.lng], { icon: customIcon })
      .addTo(map)

      .bindPopup(`<b>${values.nama_desa}</b>`);
    L.circle(latlng, {
      radius: 2000,
       color: circleColor,
    fillColor: circleColor,
      fillOpacity: 0.2,
      weight: 1,
    }).addTo(map);
  });
};

onMounted(() => {
  fetchMap();
});
</script>
