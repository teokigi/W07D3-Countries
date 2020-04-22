<template>
  <div id="app">
    <h2>Global population: {{this.totalPopulation}}</h2>

    <label for="country_select">Select a Country:</label>
    <select id="country_select" v-model="selectedCountry">
      <option disabled value="">Select a country</option>
      <option v-for="country in countries" :value="country">{{country.name}}</option>
    </select>
    <div id="countryboxes">
      <div id="selectedCount">
        <button v-on:click="appendCountry">Add Country to Favourites</button>
        <countries-list :country="selectedCountry" ></countries-list>
        <br>
        <p>Neighbouring countries list:</p>
        <neighbouring-countries-list v-for="country in neighbouringCountries" :country="country">
        </neighbouring-countries-list>
      </div>
      <div id="favourites">
        <!-- <favourite-countries-list v-for="country of neighbouringCountriesFilter" :country="country">
        </favourite-countries-list> -->
      </div>
  </div>

</div>

</template>

<script>

import CountriesList from './components/CountriesList.vue'
import FavouriteCountriesList from './components/FavouriteCountriesList.vue'
import NeighbouringCountriesList from './components/NeighbouringCountriesList.vue'

export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      favouriteCountries: [],
    }
  },
  components:{
    'countries-list': CountriesList,
    'favourite-countries-list': FavouriteCountriesList
  },
    computed: {
      totalPopulation(){
        return this.countries.reduce((total,country) => total + country.population,0); //might not work !!!
      },
      neighbouringCountriesFilter(){
          return this.selectedCountry.borders;
      }

    },
    mounted(){
      this.fetchCountry()
    },
    methods: {
      fetchCountry: function(){
        fetch("https://restcountries.eu/rest/v2/all")
        .then(response => response.json())
        .then(data => this.countries = data)
      },
      appendCountry(){
        this.favouriteCountries.push(this.selectedCountry);
      }
    }
}
</script>

<style>
.small-flag {
  height: 20px
}
div{
  border-style:solid;
  border-color:grey;
}
#countryboxes{
  width:500px;
  display:flex;
  flex-direction:row;
  justify-content:space-around;
}


</style>

<!-- Show a list of the selected country’s neighbouring countries.
Display the total population of these neighbouring countries.
Prevent the same country being added to the user’s favourite countries list twice. -->
