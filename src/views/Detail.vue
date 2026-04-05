<template>
  <div class="container mt-5 text-center">
    <div v-if="!character" class="loading-state">
      <div class="spinner-border text-light"></div>
      <p>Loading...</p>
    </div>

    <div v-else class="detail-card card shadow p-4 mx-auto">
      <h1>{{ character.name }}</h1>

      <img
        :src="character.imageUrl || 'https://via.placeholder.com/150'"
        width="250"
        class="mx-auto my-3 rounded-3"
      />

      <p><b>Films:</b> {{ character.films?.length ? character.films.join(', ') : '-' }}</p>
      <p><b>TV Shows:</b> {{ character.tvShows?.length ? character.tvShows.join(', ') : '-' }}</p>
      <p><b>Allies:</b> {{ character.allies?.length ? character.allies.join(', ') : '-' }}</p>
      <p><b>Enemies:</b> {{ character.enemies?.length ? character.enemies.join(', ') : '-' }}</p>

      <button @click="$router.push('/characters')" class="btn btn-disney mt-3">
        Back to Gallery
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      character: null
    }
  },

  mounted() {
    const id = this.$route.params.id

    fetch(`https://api.disneyapi.dev/character/${id}`)
      .then(res => res.json())
      .then(data => {
        this.character = data.data
      })
  }
}
</script>

<style scoped>
.detail-card {
  max-width: 520px;
  border-radius: 2rem;
  background: rgba(3, 20, 72, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.16);
  color: #f8f9ff;
}

.detail-card h1 {
  font-family: 'Disney', cursive;
  font-size: 2.8rem;
  margin-bottom: 1rem;
  color: #ffffff;
}

.detail-card p {
  color: #eef2ff;
}

.detail-card b {
  color: #ffffff;
}

.loading-state p {
  color: #dce2ff;
}

.btn-disney {
  background: linear-gradient(135deg, #ffce00, #e35a88);
  border: none;
  color: #111;
  padding: 0.6rem 1.4rem;
  border-radius: 999px;
}
</style>
