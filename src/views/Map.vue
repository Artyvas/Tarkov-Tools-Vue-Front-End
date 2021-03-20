<template>
  <div id="map"></div>
</template>

<style>
#map {
  height: 1500px;
  width: 1000px;
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
    // Initializes the Leaflet map - defines zooms and center
    setupLeafletMap: function() {
      var map = L.map("map", {
        maxZoom: 24,
        minZoom: 0.0,
        crs: L.CRS.Simple,
      }).setView(this.center, 0.0001);
      // Sets the maximum lat and lng for the map:
      map.setMaxBounds(new L.LatLngBounds([0, 1200], [10000, 0]));
      // Sets image as background of the leaflet map:
      var imageUrl = "trailerpark_crossroads.png";
      var imageBounds = [
        [1920, 0],
        [0, 1080],
      ];
      // Brainstorm idea as to how to make insert the appropriate icon using string stored in searchableobject variable (name of the searchableobject). Make an object that links a passed in string with an initialized icon variable - then call the variable by passing in the searchableobject name string into the object.

      // These variables toggle the px by px dimensions of the logos:
      let xSize = 20;
      let ySize = 20;

      var looseLootIcon = L.icon({
        iconUrl: "PMCExtract.png",
        iconSize: [xSize, ySize],
      });

      // Initializes all of the Map Icons as JS variables:
      // var ammoBoxIcon = L.icon({
      //   iconUrl: "ammobox.png",
      //   iconSize: [xSize, ySize],
      // });

      // var bossSpawnIcon = L.icon({
      //   iconUrl: "bossSpawn.png",
      //   iconSize: [xSize, ySize],
      // });

      // var cashRegisterIcon = L.icon({
      //   iconUrl: "cashRegister.png",
      //   iconSize: [xSize, ySize],
      // });

      // var computerIcon = L.icon({
      //   iconUrl: "computer.png",
      //   iconSize: [xSize, ySize],
      // });

      // var drawerIcon = L.icon({
      //   iconUrl: "drawer.png",
      //   iconSize: [xSize, ySize],
      // });

      // var pmcExtractIcon = L.icon({
      //   iconUrl: "PMCExtract.png",
      //   iconSize: [xSize, ySize],
      // });

      // var mixedExtractIcon = L.icon({
      //   iconUrl: "MixedExtract.png",
      //   iconSize: [xSize, ySize],
      // });

      // var scavExtractIcon = L.icon({
      //   iconUrl: "ScavExtract.png",
      //   iconSize: [xSize, ySize],
      // });

      // var grenadeBoxIcon = L.icon({
      //   iconUrl: "grenade.png",
      //   iconSize: [xSize, ySize],
      // });

      // var jacketIcon = L.icon({
      //   iconUrl: "jacket.png",
      //   iconSize: [xSize, ySize],
      // });

      // var keyIcon = L.icon({
      //   iconUrl: "key.png",
      //   iconSize: [xSize, ySize],
      // });

      // var looseLootIcon = L.icon({
      //   iconUrl: "looseloot.png",
      //   iconSize: [xSize, ySize],
      // });

      // var medBagIcon = L.icon({
      //   iconUrl: "medbag.png",
      //   iconSize: [xSize, ySize],
      // });

      // var pmcSpawnIcon = L.icon({
      //   iconUrl: "PMCSpawn.png",
      //   iconSize: [xSize, ySize],
      // });

      // var scavSpawnIcon = L.icon({
      //   iconUrl: "ScavSpawn.png",
      //   iconSize: [xSize, ySize],
      // });

      // var questItemIcon = L.icon({
      //   iconUrl: "questitem.png",
      //   iconSize: [xSize, ySize],
      // });

      // var safeIcon = L.icon({
      //   iconUrl: "safe.png",
      //   iconSize: [xSize, ySize],
      // });

      // var sportsBagIcon = L.icon({
      //   iconUrl: "sportsbag.png",
      //   iconSize: [xSize, ySize],
      // })

      // var stashIcon = L.icon({
      //   iconUrl: "stash.png",
      //   iconSize: [xSize, ySize],
      // });

      // var toolboxIcon = L.icon({
      //   iconUrl: "toolbox.png",
      //   iconSize: [xSize, ySize],
      // });

      // var weaponBoxIcon = L.icon({
      //   iconUrl: "weaponbox.png",
      //   iconSize: [xSize, ySize],
      // });

      // var scavSniperIcon = L.icon({
      //   iconUrl: "scavsniper.png",
      //   iconSize: [xSize, ySize],
      // });

      // var woodenCrateIcon = L.icon({
      //   iconUrl: "wooden-crate.png",
      //   iconSize: [xSize, ySize],
      // });

      // var deadScavIcon = L.icon({
      //   iconUrl: "deadscav.png",
      //   iconSize: [xSize, ySize],
      // });

      // Initializes icon object:

      searchableObjectIndex = {
        "Wooden Crate": woodenCrateIcon,
        "Weapon Box/Rack": weaponBoxIcon,
        Jacket: jacketIcon,
        "Loose Loot": looseLootIcon,
        "Sports Bag": sportsBagIcon,
        "Dead Scav": deadScavIcon,
        "Med Bag": medBagIcon,
        Drawers: drawerIcon,
        PC: computerIcon,
        Safe: safeIcon,
        Stash: stashIcon,
      };

      // Creates markers for searchable objects on the map:

      let i = 0;
      while (i < this.searchableobjects.length) {
        if (this.searchableobjects[i].y_coor && this.searchableobjects[i].x_coor) {
          L.marker([this.searchableobjects[i].y_coor, this.searchableobjects[i].x_coor], { icon: looseLootIcon })
            .addTo(map)
            .bindPopup(this.searchableobjects[i].description);
        }
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
