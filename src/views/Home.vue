<template>
  <div>
    <h1>Disney Characters</h1>

    <div v-for="char in characters" :key="char._id">
      <h3>{{ char.name }}</h3>
      <img :src="char.imageUrl" width="100" />

      <button @click="goDetail(char._id)">
        Detail
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characters: []
    }
  },
  mounted() {
    fetch('https://api.disneyapi.dev/character')
      .then(res => res.json())
      .then(data => {
        this.characters = data.data
      })
  },
  methods: {
    goDetail(id) {
      this.$router.push(`/detail/${id}`)
    }
  }
}
</script>