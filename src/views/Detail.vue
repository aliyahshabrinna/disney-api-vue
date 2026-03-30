<template>
  <div v-if="character">
    <h1>{{ character.name }}</h1>
    <img :src="character.imageUrl" width="200" />

    <p><b>Films:</b> {{ character.films.join(', ') }}</p>
    <p><b>TV Shows:</b> {{ character.tvShows.join(', ') }}</p>
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