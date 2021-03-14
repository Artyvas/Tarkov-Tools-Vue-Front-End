<template>
<div class="home">
<h1> All keys</h1>
<div v-for="key in keys" v-bind:key="key.id">
  <img v-bind:src="key.image_url" alt="" />
  <h2>
    Name: {{ key.name }}
  </h2>
</div>
</div>
</template>

<style>

</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      keys: [],
    };
  },
    created: function() {
      this.indexKeys();
    },
    methods: {
      indexKeys: function() {
        axios.get("/api/keys").then(response => {
          this.keys = response.data;
          console.log("All Keys:", this.keys);
        });
      },
    }
  }
</script>