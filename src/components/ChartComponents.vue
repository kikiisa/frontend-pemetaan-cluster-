<script setup>
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from 'chart.js'

// Registrasi komponen Chart.js
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

const chartData = {
  labels: ['Tinggi', 'Rendah', 'Sedang'],
  datasets: [
    {
    label: 'Jumlah User',
    backgroundColor: ['#8A0000', '#34d399', '#fbbf24'], // Warna beda per label
    data: [40, 20, 60],
    },
  ],
}

const chartOptions = {
  responsive: true,
  plugins: {
    legend: {
      position: 'top',
    },
    title: {
      display: true,
      text: 'Grafik Klaster',
    },
  },
}
</script>

<template>
  <Bar :data="chartData" :options="chartOptions" />
</template>
