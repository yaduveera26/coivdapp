<template>
  <div v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate"/>
    <DataBoxes :stats="stats"/>
  </div>
  <div class="flex justify-center align-center text-gray-500 text-3xl" v-else>
    ..... loading
  </div>
  <div class="">
    <CountrySelect @get-country="getCountryData" :countries="countries"/>
    <button @click="clearCountry" v-if="stats.Country" type="button" class="bg-green-700 text-white rounded m-5 px-7 font-bold py-3 hover:bg-green-500" name="button">
      Clear
    </button>
  </div>
</template>

<script>

import DataTitle from '@/components/Datatitle'
import DataBoxes from '@/components/Databoxes'
import CountrySelect from '@/components/Country'

export default {
  name: 'Home',
  components:{
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data()
  {
    return{
      loading:true,
      title:'Global',
      dataDate:'',
      stats:{},
      countries:[],
    }
  },
  methods:{
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    },
    getCountryData(country){
      this.stats = country
      this.title = country.Country
    },
    async clearCountry()
    {
      this.loading = true
      const data = await this.fetchCovidData()
      this.stats = data.Global
      this.title = 'Global'
      this.loading = false
    }
  },
  async created(){
      const data = await this.fetchCovidData()
      console.log(data);
      this.dataDate = data.Date
      this.stats = data.Global
      this.countries = data.Countries
      this.loading = false
  }
}
</script>
