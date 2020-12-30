<template>
  <div class="container">
    <h1>緯度経度検索</h1>
    <p>土地名：{{ place }}</p>
    <p>住所：{{ address }}</p>
    <p>緯度：{{ lat }}</p>
    <p>経度：{{ lng }}</p>
    <!-- <form> -->
      <input type="text" name="place" id="place" v-model="place">
      <button @click="search">検索</button>
    <!-- </form> -->
  </div>
</template>

<script>
const axios = require('axios');

const GEOCODE_ENDPOINT = 'https://maps.googleapis.com/maps/api/geocode/json';

export default {
  data: function () {
    return {
      place: '',
      address: '',
      lat: null,  //緯度
      lng: null,  //経度
    }
  },
  methods: {
    search: function () {
      axios.get(GEOCODE_ENDPOINT, {
        params: {
          address: this.place,
          key: process.env.GOOGLE_API_KEY,
        }
      }).then(res => {
          console.log(res);
          this.address = res.data.results[0].formatted_address;
          this.lat = res.data.results[0].geometry.location.lat;
          this.lng = res.data.results[0].geometry.location.lng;
        }).catch(err => {
          console.log(err);
        });
    }
  }
}
</script>

<style>
</style>
