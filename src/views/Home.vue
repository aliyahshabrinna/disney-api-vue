<template>
  <div class="container mt-4">
    <h1 class="text-center mb-4">Disney Characters</h1>

    <!-- LOADING -->
    <div v-if="loading" class="text-center">
      <div class="spinner-border text-light"></div>
    </div>

    <!-- CONTENT -->
    <div v-else>

      <!-- SEARCH (CENTER) -->
      <div class="row justify-content-center mb-4">
       <div class="col-md-6">
        <div class="input-group">
          <input v-model="search" class="form-control" placeholder="Cari karakter..." />
      <button @click="searchCharacter" class="btn btn-primary">Search</button>
    </div>
  </div>
</div>

      <!-- DATA -->
      <div class="row justify-content-center">
        <div class="col-3 mb-4 d-flex" v-for="char in characters" :key="char._id">
          <div class="card character-card shadow h-100 text-center">

            <img 
              :src="char.imageUrl || 'https://via.placeholder.com/150'" 
              class="card-img-top"
              style="height:200px; object-fit:cover;"
            />

            <div class="card-body">
              <h5>{{ char.name }}</h5>

              <button 
                @click="goDetail(char._id)" 
                class="btn btn-primary btn-sm mt-2"
              >
                Detail
              </button>
            </div>

          </div>
        </div>
      </div>

      <!-- PAGINATION -->
      <div class="text-center">
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

<style>
@font-face {
  font-family: 'Disney';
  src: url('/fonts/waltographUI.ttf') format('truetype');
}

body {
  font-family: 'Quicksand', sans-serif;
  background: linear-gradient(to bottom, #BCEFFF, #01147C);
  color: white;
}

/* efek bintang */
body::before {
  content: "";
  position: fixed;
  width: 100%;
  height: 100%;
  background: url("https://www.transparenttextures.com/patterns/stardust.png");
  opacity: 0.3;
  z-index: -1;
}

/* judul */
h1 {
  font-family: 'Disney', cursive;
  font-size: 50px;
  text-align: center;
}

/* card */
.card {
  background: hsla(206, 84%, 73%, 0.85);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  color: white;
  height: 100%;
}

/* body card biar rata */
.card-body {
  min-height: 120px;
}

/* hover */
.character-card {
  transition: 0.4s;
}

.character-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 0 20px #BCEFFF;
}

button {
  border-radius: 20px;
}

.btn-secondary {
  background-color: #6db2dc;
  border-color: #6db2dc;
}
</style>