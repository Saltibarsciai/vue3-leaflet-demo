<template>
    <div style="height: 50vh; width: 50vw;">
        <l-map
                v-model="zoom"
                v-model:zoom="zoom"
                :center="[47.41322, -1.219482]"
                @move="log('move')"
        >
            <l-tile-layer
                    url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
            ></l-tile-layer>
            <l-marker
                    ref="marker"
                    :lat-lng="[0, 0]"
                    :icon="iconOne"
                    draggable
                    @moveend="log('moveend')"
            ></l-marker>
        </l-map>
    </div>
  <button @click="changeIcon">
    change icon
  </button>
</template>
<script>
    import {LMap, LTileLayer, LMarker} from "@vue-leaflet/vue-leaflet";
    import L from "leaflet"
    import "leaflet/dist/leaflet.css";

    export default {
        components: {
            LMap,
            LTileLayer,
            LMarker,
        },
        data() {
            return {
                zoom: 2,
            };
        },
        methods: {
            log(a) {
                console.log(a);
            },
          changeIcon() {
              this.$refs['marker'].icon.options.iconUrl = 'g.jpg'
          }
        },
        computed: {
            iconOne() {
                return L.icon({
                    iconUrl: 'e.jpg',
                    iconSize: [51, 58],
                })
            },
            iconTwo() {
                return L.icon({
                    iconUrl: 'g.jpg',
                    iconSize: [51, 58],
                })
            }
        }
    };
</script>
