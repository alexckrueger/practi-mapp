<script>
/* global L*/
export default {
  data: function () {
    return {
      message: "This is my mapp app",
      locations: [
        { name: "Zazas Pizzeria", latitude: 41.93742, longitude: -87.6483 },
        { name: "Gordon Ramsay Burger", latitude: 41.89339, longitude: -87.628 },
        { name: "Friends Station", latitude: 41.89686075995737, longitude: -87.62836438435944 },
        { name: "Little Wok Wicker Park", latitude: 41.90351, longitude: -87.6768 },
        { name: "Peanut Park Trattoria", latitude: 41.86911, longitude: -87.66147 },
      ],
    };
  },
  created: function () {},
  mounted: function () {
    var map = L.map("map").setView([41.8781, -87.6298], 13);
    L.tileLayer("https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}", {
      attribution:
        'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
      maxZoom: 18,
      id: "mapbox/streets-v11",
      tileSize: 512,
      zoomOffset: -1,
      accessToken: process.env.VUE_APP_MAP_API,
    }).addTo(map);
    var marker = L.marker([41.8781, -87.6298]).addTo(map);
    marker.bindPopup("<b>Hello world!</b><br>or just Chicago!<br>This is the initial center.");
    var popup = L.popup();

    function onMapClick(e) {
      popup
        .setLatLng(e.latlng)
        .setContent("You clicked the map at " + e.latlng.toString())
        .openOn(map);
      map.setView(e.latlng);
    }

    map.on("click", onMapClick);

    this.locations.forEach((location) => {
      var marker = L.marker([location.latitude, location.longitude]).addTo(map);
      marker.bindPopup(location.name);
    });
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>There are many like it, but this one is mine.</p>
    <br />
    <br />
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  height: 500px;
}
</style>
