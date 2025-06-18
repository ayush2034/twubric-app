<template>
  <div class="date-filter d-flex flex-column flex-md-row align-items-md-center gap-3">
    <div>
      <label class="form-label">Start Date</label>
      <input type="date" class="form-control" v-model="start" />
    </div>
    <div>
      <label class="form-label">End Date</label>
      <input type="date" class="form-control" v-model="end" />
    </div>
    <button class="btn btn-primary mt-2 mt-md-4" @click="applyFilter">Apply</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const emit = defineEmits(['filter'])

const start = ref('')
const end = ref('')

function applyFilter() {
  emit('filter', { start: start.value, end: end.value })
}
</script>

<style scoped>
.date-filter {
  background-color: #ffffff;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.05);
}
.form-label {
  font-weight: 500;
}
</style>
