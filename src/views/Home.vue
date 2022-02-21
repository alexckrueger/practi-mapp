<script>
/* global L*/
export default {
  data: function () {
    return {
      message: "This is my mapp app",
      map: "",
    };
  },
  created: function () {},
  methods: {},
  mounted: function () {
    this.map = L.map("map").setView([41.8781, -87.6298], 13);
    L.tileLayer("https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}", {
      attribution:
        'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
      maxZoom: 18,
      id: "mapbox/streets-v11",
      tileSize: 512,
      zoomOffset: -1,
      accessToken: process.env.VUE_APP_MAP_API,
    }).addTo(this.map);
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  height: 500px;
}
</style>
