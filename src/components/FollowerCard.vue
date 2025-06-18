<template>
  <div class="card follower-card">
    <img :src="user.image" class="avatar" alt="User Image" />
    <div class="info">
      <h5 class="name">{{ user.fullname }}</h5>
      <p class="username">@{{ user.username }}</p>
      <p class="joined">Joined: {{ formatJoinDate(user.join_date) }}</p>
      <ul class="scores">
        <li><strong>Friends:</strong> {{ user.twubric.friends }}</li>
        <li><strong>Influence:</strong> {{ user.twubric.influence }}</li>
        <li><strong>Chirpy:</strong> {{ user.twubric.chirpiness }}</li>
        <li><strong>Total:</strong> {{ user.twubric.total }}</li>
      </ul>
      <button class="btn btn-danger remove-btn" @click="$emit('remove', user.uid)">
        Remove
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps(['user'])

function formatJoinDate(timestamp) {
  return new Date(timestamp * 1000).toLocaleDateString()
}
</script>

<style scoped>
.follower-card {
  display: flex;
  flex-direction: column;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 12px;
  padding: 1rem;
  transition: box-shadow 0.3s ease;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.04);
}

.follower-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
}

.avatar {
  width: 100%;
  max-width: 120px;
  height: auto;
  border-radius: 50%;
  align-self: center;
  margin-bottom: 1rem;
}

.info {
  display: flex;
  flex-direction: column;
  text-align: center;
}

.name {
  font-size: 1.25rem;
  font-weight: bold;
  margin-bottom: 0.25rem;
}

.username {
  color: #777;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.joined {
  font-size: 0.85rem;
  color: #888;
  margin-bottom: 0.75rem;
}

.scores {
  list-style: none;
  padding: 0;
  margin-bottom: 1rem;
  text-align: left;
  font-size: 0.9rem;
}

.scores li {
  margin-bottom: 0.3rem;
}

.remove-btn {
  align-self: center;
  width: 100%;
  font-weight: bold;
  border-radius: 6px;
}

/* Responsive tweaks */
@media (min-width: 576px) {
  .follower-card {
    flex-direction: row;
    align-items: center;
    gap: 1rem;
  }

  .avatar {
    margin-bottom: 0;
    width: 100px;
  }

  .info {
    flex: 1;
    text-align: left;
  }

  .remove-btn {
    max-width: 150px;
  }
}
</style>
