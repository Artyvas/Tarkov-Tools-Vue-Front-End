<template>
  <div id="map"></div>
</template>

<style>
#map {
  height: 750px;
  width: 500px;
}
</style>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import axios from "axios";

export default {
  name: "map",
  data() {
    return {
      center: [200, 200],
      searchableobjects: [],
    };
  },
  methods: {
    setupLeafletMap: function() {
      var map = L.map("map", {
        maxZoom: 24,
        minZoom: 0.0000001,
        crs: L.CRS.Simple,
      }).setView(this.center, 0.0001);

      map.setMaxBounds(new L.LatLngBounds([0, 10000], [10000, 0]));

      var imageUrl = "trailerpark_crossroads.png";
      var imageBounds = [
        [1920, 0],
        [0, 1080],
      ];
      var skullIcon = L.icon({
        iconUrl: "iconfinder_Skull_1531895.png",
        iconSize: [20, 20],
      });
      // Loop through this.searchableobjects
      let i = 0;
      while (i < this.searchableobjects.length) {
        console.log(this.searchableobjects[i]);
        console.log(this.searchableobjects[i].y_coor);
        L.marker([this.searchableobjects[i].y_coor, this.searchable_objects[i].x_coor], { icon: skullIcon })
          .addTo(map)
          .bindPopup(this.searchableobjects[i].description);
        i++;
      }

      L.imageOverlay(imageUrl, imageBounds).addTo(map);
    },
  },
  mounted() {
    axios.get("/api/searchableobjects").then(response => {
      this.searchableobjects = response.data;
      console.log("All SearchableObjects:", this.searchableobjects);
      this.setupLeafletMap();
    });
  },
};
</script>
