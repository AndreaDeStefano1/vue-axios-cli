<template>
  <div>

    <div class="container" v-if="isLoaded">
      <SearchbarComp @search='coffeeToSearch'/>
      <CoffeeComp
      v-for="coffee in filteredCoffeeList" :key="coffee.id"
      :coffeItem="coffee"/>
    </div>
    <div class="container" v-else>
      <LoaderComp loaderName="LOADING CAFFE"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CoffeeComp from './components/CoffeeComp.vue';
import LoaderComp from './components/LoaderComp.vue';
import SearchbarComp from './components/SearchbarComp.vue';

export default {
  name: 'App',
  data(){
    return{
      baseURL:'https://api.sampleapis.com/coffee/hot',
      coffeeArray:[],
      isLoaded : false,
      coffeeTextToSearch: '',
    }
  },
  components: {
    CoffeeComp,
    LoaderComp,
    SearchbarComp
},
  mounted(){
    this.getAPI()
  },
  methods:{
    getAPI(){
     axios.get(this.baseURL)
     .then(r => {
       this.coffeeArray = r.data;
       console.log(r.data);
        this.isLoaded = true
     })
    },
    coffeeToSearch(textToSearch){
      // console.log(textToSearch);
      this.coffeeTextToSearch = textToSearch;
    },
  },
  computed:{
    filteredCoffeeList(){
      let filteredArray = [];
      if(this.coffeeTextToSearch.length == 0){
        filteredArray = this.coffeeArray
      }else{
        filteredArray = this.coffeeArray.filter(coffee => {
          return coffee.title.toUpperCase().includes(this.coffeeTextToSearch.toUpperCase())
        })
      }
      return filteredArray;
    }
  }
}
</script>

<style lang="scss">
@import './assets/style/general'

</style>
