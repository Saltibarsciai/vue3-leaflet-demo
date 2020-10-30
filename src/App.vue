<template>
    <div>
        <div style="height: 50vh; width: 50vw;">
            <l-map
                    v-model="zoom"
                    v-model:zoom="zoom"
                    :center="[47.41322, -1.219482]"
                    ref="map"
            >
                <l-tile-layer
                        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
                ></l-tile-layer>
                <l-marker
                        ref="marker"
                        :lat-lng="[0, 0]"
                        :icon="iconOne"
                >
                    <l-popup>
                        hello
                    </l-popup>
                </l-marker>
                <l-marker
                        ref="marker2"
                        :lat-lng="[20, 4]"
                >
                    <l-popup>
                        hellooo
                    </l-popup>
                </l-marker>
            </l-map>
        </div>
        <button @click="changeIcon">
            change icon
        </button>
    </div>
</template>
<script>
    import {LMap, LTileLayer, LMarker, LPopup} from "@vue-leaflet/vue-leaflet";
    import L from "leaflet"
    import "leaflet/dist/leaflet.css";

    export default {
        components: {
            LMap,
            LTileLayer,
            LMarker,
            LPopup
        },
        data() {
            return {
                zoom: 2,
                map: [],
                marker: []
            };
        },
        mounted() {
            // this.testVersion012();
            // this.testVersion020();
        },
        methods: {
            testVersion012() {
                //have to double $nextTick to get this.$refs.map.mapObject
                this.$nextTick(() => {
                    this.$nextTick(() => {
                        //bind mapObject ref to data object
                        this.map = this.$refs.map.mapObject;
                        //show map ref named "map"
                        console.log('map ref - ', this.$refs.map);
                        //show mapObject
                        console.log('mapObject of map ref - ', this.$refs.map.mapObject);
                        //remove ability to zoom when scrolling from map
                        this.map.scrollWheelZoom.disable();
                        //remove default zoom controls in order to create vustom ones
                        this.map.zoomControl.remove();
                        //add scale to map
                        L.control.scale().addTo(this.map);
                        //add custom control to the right side
                        L.control.zoom({position: 'topright'}).addTo(this.map);

                        this.map.on('popupopen', () => {
                            console.log('event popup open')
                        });
                        this.map.on('popupclose', () => {
                            console.log('event popup close')
                        });
                        this.map.on('dragend', () => {
                            console.log('get bound when map moved', this.map.getBounds());
                        });
                        this.map.on('zoomend', () => {
                            console.log('get bound when map zoomed', this.map.getBounds());
                        });
                    });
                });
            },
            testVersion020(){
                //have to double $nextTick to get this.$refs.map.mapObject
                this.$nextTick(() => {
                    this.$nextTick(() => {
                        //bind mapObject ref to data object
                        this.map = this.$refs.map.leafletObject;
                        //show map ref named "map"
                        console.log('map ref - ', this.$refs.map);
                        //show mapObject
                        console.log('mapObject of map ref - ', this.$refs.map.leafletObject);
                        //remove ability to zoom when scrolling from map
                        this.map.scrollWheelZoom.disable();
                        //remove default zoom controls in order to create vustom ones
                        this.map.zoomControl.remove();
                        //add scale to map
                        L.control.scale().addTo(this.map);
                        //add custom control to the right side
                        L.control.zoom({position: 'topright'}).addTo(this.map);

                        this.map.on('popupopen', () => {
                            console.log('event popup open')
                        });
                        this.map.on('popupclose', () => {
                            console.log('event popup close')
                        });
                        this.map.on('dragend', () => {
                            console.log('get bound when map moved', this.map.getBounds());
                        });
                        this.map.on('zoomend', () => {
                            console.log('get bound when map zoomed', this.map.getBounds());
                        });
                    });
                });
            },
            testVersion020Click(){
                this.map = this.$refs.map.leafletObject;
                this.map.scrollWheelZoom.disable();
                //remove default zoom controls in order to create vustom ones
                this.map.zoomControl.remove();
                //add scale to map
                L.control.scale().addTo(this.map);
                //add custom control to the right side
                L.control.zoom({position: 'topright'}).addTo(this.map);
                console.log(this.$refs.map.leafletObject)
            },
            changeIcon() {
                //how to change icon via refs?
                console.log('change shrek icon to kitten', this.$refs['marker'])
                this.$refs['marker'].icon.options.iconUrl = 'g.jpg';
                this.testVersion020Click();
            }
        },
        computed: {
            iconOne() {
                return L.icon({
                    iconUrl: 'e.jpg',
                    iconSize: [51, 58],
                })
            }
        }
    };
</script>
