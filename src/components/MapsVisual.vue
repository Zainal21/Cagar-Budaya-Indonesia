<template>
  <div class="maps-container">
    <LMap :zoom="zoom" :center="center">
      <LTileLayer :url="url"></LTileLayer>
      <ul>
        <li v-for="(coordinates ,index ) in latlong" :key="index">
          <LMarker :lat-lng="coordinates" />
        </li>
      </ul>
    </LMap>

    <div class="container xm-auto  py-10">
      <div class="mx-auto mb-10 lg:max-w-xl">
        <h2
          class="inline-block px-3 py-px text-xl font-semibold tracking-wider text-teal-900 uppercase rounded-full bg-teal-accent-400">
          Daftar Lokasi Cagar Budaya
        </h2>
      </div>
      <div class="flex justify-center">
        <div class="mb-3 xl:w-96">
          <select class="form-select appearance-none
          block
          w-full
          px-3
          py-1.5
          text-base
          font-normal
          text-gray-700
          bg-white bg-clip-padding bg-no-repeat
          border border-solid border-gray-300
          rounded
          transition
          ease-in-out
          m-0
          focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
            aria-label="Default select example"
            v-model="code_region"
             @change="getItemLocation()">
            <option disabled value="">Pilih Provinsi</option>
            <option 
                v-for="province in Provinces" 
                :key="province.kode_wilayah" 
                :value="province.kode_wilayah">
                {{province.nama}}
            </option>
          </select>
        </div>
      </div>
      <ListCagarBudaya :listItemCagarBudaya="listItemCagarBudaya" />
    </div>
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
  const BASE_API_URL = 'https://api-cagar-budaya.vercel.app/api/'
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
        zoom: 5,
        center: [-0.789275, 113.921327],
        bounds: null,
        latlong: [],
        listItemCagarBudaya: [],
        Provinces: [],
        code_region:''
      }
    },
    onReady(mapObject) {
      mapObject.locate();
    },
    onLocationFound(location) {
      console.log(location)
    },
    mounted: function () {
      this.getItemLocation(),
        this.getProvinces()
    },
    methods: {
      getItemLocation() {
        axios.get(`${BASE_API_URL}cagar-budaya?kode_wilayah=${this.code_region}`)
          .then(response => response.data)
          .then(response => {
            let result = response.data
            this.listItemCagarBudaya = result
            this.latlong = [];
            result.map(item => {
              let coordinate = []
              coordinate.push(parseFloat(item.lintang))
              coordinate.push(parseFloat(item.bujur))
              this.latlong.push(coordinate)
            })
          })
        console.log(this.latlong)
        console.clear()
      },
      getProvinces() {
        axios.get(`${BASE_API_URL}provinces`)
          .then(response => response.data)
          .then(response => {
            this.Provinces = response.data
          })
          console.clear()
      }
    }
  }
</script>


<style scoped>
  .maps-container {
    height: 50vh;
  }
</style>