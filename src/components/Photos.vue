<template>
  <div>
    <div class="jumbotron position-fixed fixed-top row" v-if="albumLoaded">
      <h1 class="col-12 col-lg-8"><b>Album:</b> {{album.title}}</h1>
      <router-link  class="col-12 col-lg-4" :to="'/'">
        <button class="btn btn-dark">
          Go back to see all albums
        </button>
      </router-link>
    </div>
    <div class="d-flex flex-wrap justify-content-center photos mx-5">
      <div v-for="photo in photos" v-bind:key="photo.id" class="m-5">
        <div class="card">
          <div class="card-img-top">
            <img class="photo" v-bind:src="photo.url">
          </div>
          <div class="card-text">
            {{photo.title}}
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
      albumId: '',
      album: {},
      albumLoaded: false,
      photos: []
    }
  },
  methods: {
    getPhotos (albumId) {
      this.$http.get(`https://jsonplaceholder.typicode.com/photos?albumId=${albumId}`)
        .then((response) => {
          this.photos = response.data
        })
        .catch(() => {
          alert('Upsss, something went wrong. Try again later')
        })
    },
    getAlbumInfo (albumId) {
      this.$http.get(`https://jsonplaceholder.typicode.com/albums/${albumId}`)
        .then((response) => {
          this.album = response.data
          this.albumLoaded = true
        })
        .catch(() => {
          alert('Upsss, something went wrong. Try again later')
        })
    }
  },
  created () {
    this.albumId = this.$route.params.id
    this.getAlbumInfo(this.albumId)
    this.getPhotos(this.albumId)
  }
}
</script>

<style scoped>
  .photo {
    width: 200px;
    height: 200px;
  }
  .photos {
    margin-top: 200px;
  }
  .card {
    width: 200px;
    box-shadow:  3px 3px 15px #929292;
  }
</style>
