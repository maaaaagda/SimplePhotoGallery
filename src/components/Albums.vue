<template>
  <div class="">
    <div class="row">
      <div class="col jumbotron">
        <h1>My favourite photo albums </h1>
        <p>Click on any of them below to see the photos</p>
      </div>
    </div>
    <div class="row">
      <div class="d-flex flex-wrap justify-content-center">
        <div class="card m-5" v-for="album in myAlbums" v-bind:key="album.id" @click="showPhotos(album.id)">
          <div class="card-body d-flex align-items-center">
            {{album.title}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      myAlbums: [],
      userId: 1
    }
  },
  methods: {
    getAllAlbums () {
      this.$http.get(`https://jsonplaceholder.typicode.com/albums?userId=${this.userId}`)
        .then((response) => {
          this.myAlbums = response.data
        })
    },
    showPhotos (albumId) {
      this.$router.push(`/albums/${albumId}`)
    }
  },
  created () {
    this.getAllAlbums()
  }
}
</script>

<style scoped>
  .card-body {
    height: 100px;
    width: 300px;
    box-shadow: 5px 5px 25px #96b8d3;
  }
  .card:hover {
    transition: all 0.5s ease-in-out;
    transform: scale(1.2);
    cursor: pointer;
  }
</style>
