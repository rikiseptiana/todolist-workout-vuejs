<!-- src/views/HomeView.vue -->
<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center">
    <div class="text-center">
      <h1 class="text-4xl font-bold mb-4">Selamat Datang di Latihan Tracker</h1>
      <router-link to="/workout">
        <button
          class="bg-blue-500 text-white px-6 py-3 rounded-lg hover:bg-blue-600"
        >
          Mulai Latihan
        </button>
      </router-link>
    </div>
  </div>
</template>

<script setup></script>
