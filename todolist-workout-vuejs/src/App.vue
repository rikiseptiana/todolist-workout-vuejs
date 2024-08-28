<!-- src/App.vue -->
<template>
  <div id="app">
    <!-- Header / Navbar -->
    <Header />

    <!-- Router View untuk menampilkan komponen berdasarkan rute -->
    <main class="container mx-auto py-6">
      <router-view />
    </main>

    <!-- Footer -->
    <Footer />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
</script>

<style scoped>
/* Gaya tambahan jika diperlukan */
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* Agar footer selalu di bawah */
}
</style>
