<template>
<div class="home">
<h1> All keys</h1>

Search by Key name: <input v-model="nameFilter" type="text">
<div v-for="key in filterBy(keys, nameFilter, 'name')" v-bind:key="key.id">
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
import Vue2Filters from 'vue2-filters'

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      keys: [],
      nameFilter: ""
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