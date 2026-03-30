<template>
  <div>
    <h1>Disney Characters</h1>

    <!-- SEARCH -->
    <input v-model="search" placeholder="Cari karakter..." />
    <button @click="searchCharacter">Search</button>
    <button @click="getAll">Reset</button>

    <!-- LIST DATA -->
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
      characters: [],
      search: ''
    }
  },

  mounted() {
    this.getAll()
  },

  methods: {
    // ambil semua data
    getAll() {
      fetch('https://api.disneyapi.dev/character')
        .then(res => res.json())
        .then(data => {
          this.characters = data.data
        })
    },

    // search data
    searchCharacter() {
      fetch(`https://api.disneyapi.dev/character?name=${this.search}`)
        .then(res => res.json())
        .then(data => {
          this.characters = data.data
        })
    },

    // ke halaman detail
    goDetail(id) {
      this.$router.push(`/detail/${id}`)
    }
  }
}
</script>