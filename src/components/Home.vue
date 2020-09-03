<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <div>
          <v-simple-table>
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left">Brgy</th>
                  <th class="text-left">Active Cases</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(baranggay, index) in baranggays" :key="index">
                  <td>{{ baranggay.name }}</td>
                  <td>{{ baranggay.activeCases }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </div>
      </v-col>

      <v-col cols="8">
        <div style="height: 450px; width: 100%">
          <div style="height: 200px overflow: auto;">
            <!-- <p>First marker is placed at {{ withPopup.lat }}, {{ withPopup.lng }}</p>
      <p>Center is at {{ currentCenter }} and the zoom is: {{ currentZoom }}</p> -->
            <!-- <button @click="showLongText">
        Toggle long popup
      </button>
      <button @click="showMap = !showMap">
        Toggle map
      </button> -->
          </div>
          <l-map
            :zoom="zoom"
            :center="center"
            :options="mapOptions"
            style="height: 100%"
            @update:center="centerUpdate"
            @update:zoom="zoomUpdate"
          >
            <l-tile-layer :url="url" :attribution="attribution" />

            <l-marker
              v-for="(baranggay, index) in baranggays"
              :key="index"
              :lat-lng="baranggay.location"
            >
              <l-tooltip :options="{ permanent: true, interactive: true }">
                <div @click="innerClick">
                  Brgy: {{ baranggay.name }} | Cases:
                  {{ baranggay.activeCases }}
                </div>
              </l-tooltip>
            </l-marker>
          </l-map>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LPopup, LTooltip } from "vue2-leaflet";

export default {
  name: "Home",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LTooltip
  },

  data: () => ({
    zoom: 13,
    center: latLng(14.1699, 121.2441),
    url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    attribution:
      '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    withPopup: latLng(14.1699, 121.2441),
    withTooltip: latLng(47.41422, -1.250482),
    currentZoom: 11.5,
    currentCenter: latLng(14.1699, 121.2441),
    showParagraph: false,
    mapOptions: {
      zoomSnap: 0.5
    },
    showMap: true,

    /*  anos: latLng(14.1743, 121.2312),
    batongMalake: latLng(14.1643, 121.2385),
    sanAntonio: latLng(14.1757, 121.2482), */

    baranggays: [
      {
        name: "Batong Malake",
        location: latLng(14.1643, 121.2385),
        activeCases: 3,
        expired: 0
      },
      {
        name: "Malinta",
        location: latLng(14.1857, 121.2326),
        activeCases: 5,
        expired: 0
      },
      {
        name: "San Antonio",
        location: latLng(14.1757, 121.2482),
        activeCases: 4,
        expired: 0
      }
    ]
  }),

  methods: {
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    showLongText() {
      this.showParagraph = !this.showParagraph;
    },
    innerClick() {
      alert("Click!");
    }
  }
};
</script>
