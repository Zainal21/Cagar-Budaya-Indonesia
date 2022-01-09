<template>
  <div class="maps-container">
    <LMap :zoom="zoom" :center="center">
      <LTileLayer :url="url"></LTileLayer>
      <ul>
        <li v-for="(coordinates ,index ) in latlong" :key="index">
          <LMarker 
            :lat-lng="coordinates"
          />
        </li>
      </ul>
    </LMap>
    <ListCagarBudaya 
      :listItemCagarBudaya="listItemCagarBudaya"
    />
  </div>
</template>


<script>
  import {
    LMap,
    LMarker,
    LTileLayer
  } from 'vue2-leaflet'
  import axios from 'axios'
  import ListCagarBudaya from './ListCagarBudaya.vue'
  export default {
    name: 'MapsVisual',
    components: {
      LMap,
      LMarker,
      LTileLayer,
      ListCagarBudaya
    },
    data: function () {
      return {
        url: "https://{s}.tile.osm.org/{z}/{x}/{y}.png",
        zoom: 8,
        center: [-7.614529, 110.712247],
        bounds: null,
        latlong: [],
        listItemCagarBudaya:[]
      }
    },
    onReady(mapObject) {
      mapObject.locate();
    },
    onLocationFound(location) {
      console.log(location)
    },
    mounted: function () {
      axios.get('https://api-cagar-budaya.vercel.app/api/cagar-budaya?kode_wilayah=030000')
        .then(response => response.data)
        .then(response => {
          let result = response.data
          this.listItemCagarBudaya = result
          result.map(item => {
            let coordinate = []
            coordinate.push(parseFloat(item.lintang))
            coordinate.push(parseFloat(item.bujur))
            this.latlong.push(coordinate)
          })
        })
      console.log(this.latlong)
    }
  }
</script>


<style scoped>
  .maps-container {
    height: 80vh;
  }
</style>