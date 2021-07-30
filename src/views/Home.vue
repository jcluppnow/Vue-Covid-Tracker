<template>
  <!-- Conditional rendering for if data has been loaded. -->
  <!-- If its not loading we are ready to render our data. -->
  <div>
    <main v-if="!loading">
      <!-- V-Bind text prop to title field in data. Do the same for dataDate. -->
      <DataTitle :text="title" :dataDate="dataDate"/>

      <!-- V-Bind stats prop to stats field from data. -->
      <DataBoxes :stats="stats"/>
      
      <!-- V-Bind counties prop to countries field from data. -->
      <CountrySelect @get-country="getCountryData" :countries="countries"/>

      <button @click="clearCountry" 
      v-if="stats.Country" 
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
        Clear Country
      </button>
    </main>
    <!-- If loading has been set, the data will be shown using this main. -->
    <main class="flex flex-col align-center justify-center text-center" v-else>
      <div class="text-gray-500 text-3xl mt-10 mb-6">
        Fetching Data
      </div>
      <!-- : is used to bind to loading image data property. -->
      <img :src="loadingImage" class="width-24 m-auto" alt=""/>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data() {
    return {
      //Loading state to not display data until its fetched.
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    async fetchCovidData() {
      const response = await fetch('https://api.covid19api.com/summary');
      const data = await response.json();

      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      //Refetch the country data.
      this.loading = true;
      //Refetch the covid data using the existing method.
      const data = this.fetchCovidData();
      this.title = 'Global';
      this.stats = data.Global;
      this.loading = false;
    }
  },
  //Async and await are needed due to the promise inside fetchCovidData.
  //Lifecycle method that runs straight away when this component is created. 
  async created() {
    //This is where we want to make our initial request for data.
    const data = await this.fetchCovidData();

    //Assign the data.
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  }
}
</script>
