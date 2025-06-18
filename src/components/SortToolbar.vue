<!-- src/components/SortToolbar.vue -->
<template>
  <div class="sort-toolbar">
    <label class="me-2">Sort By:</label>
    <button
      v-for="criterion in criteria"
      :key="criterion.key"
      :class="['btn', isActive(criterion.key) ? 'btn-primary' : 'btn-outline-primary']"
      @click="toggleSort(criterion.key)"
    >
      {{ criterion.label }}
      <span v-if="isActive(criterion.key)">
        {{ direction === 1 ? '↑' : '↓' }}
      </span>
    </button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue'

const emits = defineEmits(['sort'])

const activeCriterion = ref(null)
const direction = ref(1)

const criteria = [
  { key: 'score', label: 'Twubric Score' },
  { key: 'friends', label: 'Friends' },
  { key: 'influence', label: 'Influence' },
  { key: 'chirpy', label: 'Chirpiness' }
]

function toggleSort(criterion) {
  if (activeCriterion.value === criterion) {
    direction.value *= -1
  } else {
    activeCriterion.value = criterion
    direction.value = 1
  }

  emits('sort', {
    criterion: activeCriterion.value,
    direction: direction.value
  })
}

function isActive(criterion) {
  return activeCriterion.value === criterion
}
</script>

<style scoped>
.sort-toolbar {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex-wrap: wrap;
}
</style>
