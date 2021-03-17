<template>
  <div class="home">
    <!-- <h1>All keys</h1> -->
    <!-- Search by Key name:
    <input v-model="nameFilter" type="text" list="key-names" />
    <datalist id="key-names">
      <option v-for="key in keys" v-bind:key="key.id">{{ key.name }}</option>
    </datalist>
    <div
      is="transition-group"
      class="row"
      appear
      enter-active-class="animated fadeIn"
      leave-active-class="animated fadeOut"
    > -->
    <div class="card shadow mb-4">
      <!-- <div class="card-header py-3"></div> -->
      <div class="card-body">
        <div class="table-responsive">
          <div id="dataTable_wrapper" class="dataTables_wrapper dt-bootstrap4">
            <div class="row" id="dataTables_header">
              <div class="col-sm-6 col md-6">
                <h1 class="m-0 font-weight-bold text-primary">Tarkov Key Tool</h1>
              </div>
              <div class="col-sm-6 col-md-6">
                <div id="dataTable_filter" class="dataTables_filter">
                  <label>
                    Search:
                    <input v-model="nameFilter" type="text" list="key-names" aria-controls="dataTable" />
                    <datalist id="key-names">
                      <option v-for="key in keys" v-bind:key="key.id">{{ key.name }}</option>
                    </datalist>
                  </label>
                </div>
              </div>
            </div>
          </div>

          <table class="table table-bordered" id="dataTable" width="100%" cellspacing="0">
            <thead>
              <tr>
                <th>Thumbnail</th>
                <th>Key name</th>
                <th>Key Location</th>
                <th>Lock Location</th>
                <th>Market price</th>
                <th>Trader price</th>
              </tr>
            </thead>
            <tfoot>
              <tr>
                <th>Thumbnail</th>
                <th>Key name</th>
                <th>Key Location</th>
                <th>Lock Location</th>
                <th>Market price</th>
                <th>Trader price</th>
              </tr>
            </tfoot>
            <tbody
              is="transition-group"
              class="table table-bordered"
              appear
              enter-active-class="animated fadeIn"
              leave-active-class="animated fadeOut"
            >
              <!-- <div
                is="transition-group"
                class="table table-bordered"
                appear
                enter-active-class="animated fadeIn"
                leave-active-class="animated fadeOut"
              > -->
              <tr v-for="key in filterBy(keys, nameFilter, 'name')" v-bind:key="key.id">
                <td><img id="key_image" v-bind:src="key.image_url" alt="" /></td>
                <td>{{ key.name }}</td>
                <td>{{ key.location_id }}</td>
                <td>{{ key.location_id }}</td>
                <td>{{ key.market_price }}</td>
                <td>{{ key.trader_price }}</td>
              </tr>
              <!-- </div> -->
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      keys: [],
      nameFilter: "",
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
  },
};
</script>
