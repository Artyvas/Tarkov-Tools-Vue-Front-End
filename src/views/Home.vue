<template>
  <v-hotspot
    :init-options="hotspotConfig"
    @save-data="saveData"
    @after-delete="afterDelete" />
</template>

<style></style>

<script>
import VueHotspot from "vue-hotspot";
export default {
  components: {
    "v-hotspot": VueHotspot,
  },
  data() {
    return {
      hotspotConfig: {
        image: "https://i.imgur.com/MygwBAW.png",
        editable: false,
        interactivity: "hover",
        data: [
          { Message: "A prepopulated hotspot", Title: "Vue Hotspot 1", x: 38.0, y: 45.0 },
          { Message: "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur? Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae consequatur, vel illum qui dolorem eum fugiat quo voluptas nulla pariatur?", Title: "Vue Hotspot 2", x: 70.0, y: 78.3 },
        ],
        hotspotColor: "#85ce61",
        messageBoxColor: "#409eff",
        textColor: "#333",
        opacity: 0.9,
      },
    };
  },
  methods: {
    saveData(data) {
      // Do something with the list of hotspots
      console.log(data);
    },
    afterDelete() {
      // Do something after delete
      console.log("Do something after delete ...");
    },
  },
};
</script>
