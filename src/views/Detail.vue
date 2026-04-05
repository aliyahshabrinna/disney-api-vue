<template>
  <div class="container mt-5 text-center">

    <!-- LOADING -->
    <div v-if="!character">
      <div class="spinner-border text-light"></div>
      <p>Loading...</p>
    </div>

    <!-- CONTENT -->
    <div v-else class="card shadow p-4 mx-auto" style="max-width: 500px;">
      <h1>{{ character.name }}</h1>

      <img 
        :src="character.imageUrl || 'https://via.placeholder.com/150'" 
        width="250" 
        class="mx-auto my-3"
      />

      <p><b>Films:</b> {{ character.films?.length ? character.films.join(', ') : '-' }}</p>
      <p><b>TV Shows:</b> {{ character.tvShows?.length ? character.tvShows.join(', ') : '-' }}</p>
      <p><b>Allies:</b> {{ character.allies?.length ? character.allies.join(', ') : '-' }}</p>
      <p><b>Enemies:</b> {{ character.enemies?.length ? character.enemies.join(', ') : '-' }}</p>

      <button @click="$router.push('/')" class="btn btn-secondary mt-3">
        Kembali
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