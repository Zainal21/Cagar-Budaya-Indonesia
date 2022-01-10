<template>
 
    <div class="px-4  mx-auto sm:max-w-xl md:max-w-full lg:max-w-screen-xl md:px-24 lg:px-8 ">
      <div class="grid gap-5 lg:grid-cols-2 sm:max-w-sm sm:mx-auto lg:max-w-full">
        <div class="width-42 px-8 py-4 mb-5 mx-auto bg-white rounded-lg shadow-xl" v-for="item in listItemCagarBudaya"
          :key="item.cagar_budaya_id">
          <div class="flex  items-center justify-between">
            <span class="text-md font-semibold text-gray-600 ">Kab : {{item.kabupaten_kota}}</span>
            <a
              class="px-3 py-1 text-sm font-bold text-gray-100 transition-colors duration-200 transform bg-gray-600 rounded cursor-pointer hover:bg-gray-500">
              {{item.propinsi}}</a>
          </div>
          <div class="mt-3">
            <h1 class="text-3xl font-bold text-gray-700 mb-4  hover:underline">{{item.nama}}</h1>
            <ol>
              <li class="mt-2 text-md text-gray-600 font-medium text-left"> Nomor Penetapan : <b>{{item.propinsi}}</b>
              </li>
              <li class="mt-2 text-md text-gray-600 font-medium text-left"> Tanggal Penetapan : <b>{{item.propinsi}}</b>
              </li>
              <li class="mt-2 text-md text-gray-600 font-medium text-left"> Alamat : <b>{{item.alamat_jalan}},
                  {{item.desa_kelurahan}}, {{item.kecamatan}}</b> </li>
              <li class="mt-2 text-md text-gray-600 font-medium text-left"> pengelola : <b> {{item.pengelola}}</b></li>
              <li class="mt-2 text-md text-gray-600 font-medium text-left"> Pemilik : <b>{{item.pemilik}}</b></li>
            </ol>
          </div>
        </div>
      </div>
    </div>

</template>

<script>
  export default {
    name: 'ListCagarBudaya',
    props: ['listItemCagarBudaya']
  }
</script>

<style scoped>
  .width-42 {
    width: 35rem;
  }
</style>