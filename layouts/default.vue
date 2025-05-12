<template>
    <div>
      <Header />
      <main>
        <slot />
        <NuxtPages/>
      </main>
      <Footer />
    </div>
  </template>
  
  <script setup>
  import Header from '../layouts/header.vue'
  import Footer from '../layouts/footer.vue'
  </script>
  