<script setup>
import Header from './components/header.vue'
import Body from './components/body.vue'
import Footer from './components/footer.vue'
</script>

<template>
  <div class="app">
    <Header />
    <Body />
    <Footer />
  </div>
</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background: #dbeafe;
}
</style>
