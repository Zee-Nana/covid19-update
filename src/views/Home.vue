<template>
<v-container>
  <v-card>
    <v-card-title>
      <h3>Country Status Update on Corona Virus</h3>
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
    :headers = "headers"
    :items = "countries"
      :search="search"
       :items-per-page="5"
        class="elevation-5 rgb(165, 121, 11)"
        id="menu"
    >
    </v-data-table>
  </v-card>
</v-container>
</template>

<script>
import axios from "axios";
  export default {
    data: () => ( {
        search: '',
        headers: [
          {
            text: 'Country',
            align: 'start',
            sortable: true,
            value: 'Country',
          },
          { text: 'New Confirmed', value: 'NewConfirmed' },
          { text: 'Total Confirmed', value: 'TotalConfirmed' },
          { text: 'Total Deaths', value: 'TotalDeaths' },
          { text: 'Total Recovered', value: 'TotalRecovered' },
        ],
        countries:[]
    }),

     async created() {
        let fetchCountries = await axios.get("https://api.covid19api.com/summary")
        this.countries = fetchCountries.data.Countries;
        console.log(fetchCountries);

        
    }
  }
</script>

<style scoped>
#menu{
  color: black;
}
</style>