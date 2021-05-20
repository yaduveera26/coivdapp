<template lang="html">
  <select @change="onChange()" class="form-select mx-4 my-4  block w-full border p-3 rounded" name="" v-model="selected">
    <option value="0">Select Country</option>
    <option v-for="country in countries" :value="country.ID">
      {{country.Country}}
    </option>
  </select>
</template>

<script>
export default {
  name : 'CountrySelect',
  props : ['countries'],
  data()
  {
    return {
      selected :0
    }
  },
  methods:{
    onChange(){
      const country = this.countries.find((item)=>item.ID===this.selected)
      console.log(country);

      this.$emit('get-country',country)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
