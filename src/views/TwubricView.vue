<template>
  <div class="twubric-app">
    <TwubricChartView :users="filteredUsers" />

    <div class="controls bg-light p-3 rounded shadow-sm mb-4">
      <SortToolbar @sort="handleSort" />
      <DateFilter @filter="handleDateFilter" />
    </div>

    <div class="followers-grid">
      <FollowerCard
        v-for="user in filteredUsers"
        :key="user.uid"
        :user="user"
        @remove="removeFollower"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import SortToolbar from '../components/SortToolbar.vue'
import DateFilter from '../components/DateFilter.vue'
import FollowerCard from '../components/FollowerCard.vue'
import TwubricChartView from '../components/TwubricChartView.vue'

const users = ref([])
const sortCriterion = ref(null)
const sortDirection = ref(1)
const filterRange = ref({ start: null, end: null })

onMounted(async () => {
  window.addEventListener('keyup', handleKeyShortcut)
  const res = await fetch(
    'https://gist.githubusercontent.com/pandemonia/21703a6a303e0487a73b2610c8db41ab/raw/82e3ef99cde5b6e313922a5ccce7f38e17f790ac/twubric.json'
  )
  const data = await res.json()
  users.value = data
})

onBeforeUnmount(() => {
  window.removeEventListener('keyup', handleKeyShortcut)
})

function removeFollower(uid) {
  users.value = users.value.filter((u) => u.uid !== uid)
}

function handleSort({ criterion, direction }) {
  sortCriterion.value = criterion
  sortDirection.value = direction
}

function handleDateFilter({ start, end }) {
  filterRange.value = { start, end }
}

function handleKeyShortcut(e) {
  const key = e.key.toLowerCase()
  const sortKeys = {
    f: 'friends',
    i: 'influence',
    c: 'chirpy',
    s: 'score'
  }
  if (sortKeys[key]) {
    if (sortCriterion.value === sortKeys[key]) {
      sortDirection.value *= -1
    } else {
      sortCriterion.value = sortKeys[key]
      sortDirection.value = 1
    }
  } else if (key === 'r' && filteredUsers.value.length > 0) {
    removeFollower(filteredUsers.value[0].uid)
  }
}

const filteredUsers = computed(() => {
  let result = [...users.value]

  if (filterRange.value.start && filterRange.value.end) {
    const startDate = new Date(filterRange.value.start).getTime() / 1000
    const endDate = new Date(filterRange.value.end).getTime() / 1000
    result = result.filter(
      (u) => u.join_date >= startDate && u.join_date <= endDate
    )
  }

  if (sortCriterion.value) {
    result.sort((a, b) => {
      const aVal =
        sortCriterion.value === 'score'
          ? a.twubric.total
          : a.twubric[sortCriterion.value]
      const bVal =
        sortCriterion.value === 'score'
          ? b.twubric.total
          : b.twubric[sortCriterion.value]
      return (aVal - bVal) * sortDirection.value
    })
  }

  return result
})
</script>

<style scoped>
.twubric-app {
  background-color: #f7f9fc;
  min-height: 100vh;
  padding: 2rem;
}

.controls {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.followers-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

@media (min-width: 768px) {
  .controls {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
}
</style>
