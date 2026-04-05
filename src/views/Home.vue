<template>
  <div class="container mt-5">
    <div class="page-header text-center mb-4">
      <h1>Disney Character Vault</h1>
      <p>Explore your favorite Disney characters with magical style.</p>
    </div>

    <div v-if="loading" class="text-center mb-5">
      <div class="spinner-border text-light"></div>
    </div>

    <div v-else>
      <div class="row justify-content-center mb-4">
        <div class="col-md-6">
          <div class="input-group search-box shadow-sm">
            <input v-model="search" class="form-control" placeholder="Search characters..." />
            <button @click="searchCharacter" class="btn btn-disney">Search</button>
          </div>
        </div>
      </div>

      <div class="row justify-content-center">
        <div class="col-sm-6 col-md-4 col-lg-3 mb-4 d-flex" v-for="char in characters" :key="char._id">
          <div class="card character-card shadow h-100 text-center">
            <img
              :src="char.imageUrl || 'https://via.placeholder.com/150'"
              class="card-img-top"
              style="height:220px; object-fit:cover;"
            />
            <div class="card-body d-flex flex-column align-items-center justify-content-between">
              <h5 class="mb-3">{{ char.name }}</h5>
              <button @click="goDetail(char._id)" class="btn btn-detail btn-sm mt-2">
                Detail
              </button>
            </div>
          </div>
        </div>
      </div>

      <div class="text-center mt-3">
        <button @click="prevPage" class="btn btn-secondary m-2">Prev</button>
        <button @click="nextPage" class="btn btn-secondary m-2">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characters: [],
      search: '',
      loading: false,
      page: 1
    }
  },

  mounted() {
    this.getAll()
  },

  methods: {
    getAll() {
      this.loading = true

      fetch(`https://api.disneyapi.dev/character?page=${this.page}`)
        .then(res => res.json())
        .then(data => {
          this.characters = data.data || []
          this.loading = false
        })
    },

    searchCharacter() {
      this.loading = true

      fetch(`https://api.disneyapi.dev/character?name=${this.search}`)
        .then(res => res.json())
        .then(data => {
          this.characters = data.data || []
          this.loading = false
        })
    },

    nextPage() {
      this.page++
      this.getAll()
    },

    prevPage() {
      if (this.page > 1) {
        this.page--
        this.getAll()
      }
    },

    goDetail(id) {
      this.$router.push(`/detail/${id}`)
    }
  }
}
</script>

<style scoped>
.page-header h1 {
  font-family: 'Disney', cursive;
  font-size: 3rem;
  margin-bottom: 0.5rem;
}

.page-header p {
  color: #dceeff;
  font-size: 1rem;
}

.search-box {
  border-radius: 2rem;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.18);
  background: rgba(255, 255, 255, 0.08);
}

.search-box input {
  background: transparent;
  color: white;
  border: none;
}

.search-box input::placeholder {
  color: rgba(255, 255, 255, 0.75);
}

.search-box input:focus {
  box-shadow: none;
}

.btn-disney {
  background: linear-gradient(135deg, #ffce00, #e35a88);
  border: none;
  color: #111;
  padding: 0.5rem 1.3rem;
}

.character-card {
  transition: transform 0.35s ease, box-shadow 0.35s ease;
  background: rgba(10, 23, 83, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.22);
  color: white;
}

.character-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 0 30px rgba(255, 206, 0, 0.35);
}

.character-card .card-body {
  color: #f8f9ff;
}

.character-card h5 {
  color: #fff;
}

.btn-detail {
  background: rgba(255, 255, 255, 0.95);
  color: #111;
  border-radius: 50px;
}

.btn-secondary {
  background-color: #6db2dc;
  border-color: #6db2dc;
}
</style>
