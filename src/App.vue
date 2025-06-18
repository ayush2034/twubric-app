<script setup>
import TwubricView from './views/TwubricView.vue'
</script>

<template>
  <div class="app-wrapper">
    <main class="app-content container">
      <TwubricView />
    </main>
  </div>
</template>

<style scoped>
.app-wrapper {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.app-header {
  text-align: center;
  padding: 2rem 1rem 1rem;
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  margin-bottom: 1rem;
  border-bottom: 1px solid #dee2e6;
}

.app-header h1 {
  color: #2c3e50;
  font-size: 2rem;
  font-weight: 700;
}
</style>
