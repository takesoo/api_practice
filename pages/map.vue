<template>
    <div>
        <h1>map page</h1>
        <GmapMap
            :center="maplocation"
            :zoom="zoom"
            map-type-id="terrain"
            :style="styleMap"
            clickableIcons=true
        >
        <GmapMarker
            :key="index"
            v-for="(m, index) in markers"
            :position="m.position"
            :clickable="true"
            :draggable="true"
            @click="center=m.position"
        />
        <GmapInfoWindow
            :options="infoOptions"
            :position="infoWindowPos"
            :opened="infoWinOpen"
            @closeclick="infoWinOpen = false"
        >
            <p style="color: #000">
                {{ marker.title }}
            </p>
        </GmapInfoWindow>
        </GmapMap>
    </div>
</template>

<script>
import Vue from 'vue'
import * as VueGoogleMaps from '~/node_modules/vue2-google-maps'

Vue.use(VueGoogleMaps, {
  load: {
    key: process.env.GOOGLE_API_KEY,
    libraries: 'places',
  },
})

export default {
    data(){
        return {
            maplocation:{ lng:120, lat:35 },
            zoom: 3,
            styleMap: {width: '100%', height: '90vh'},
            marker: {},
            markers: [
                {
                    title: '佐鳴湖',
                    position: { lat: 34.7054595, lng: 137.6852776 },
                },
                {
                    title: '浜名湖ガーデンパーク',
                    position: { lat: 34.7140247, lng: 137.6032967 },
                },
            ],
        }
    },
    methods: {
        onClickMarker: function (index, marker) {
            
        }
    }
}
</script>

<style scoped>

</style>