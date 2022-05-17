<template>
  <div>
    <div class="container" v-if="isLoaded">
      <CoffeeComp
      v-for="coffee in coffeeArray" :key="coffee.id"
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

export default {
  name: 'App',
  data(){
    return{
      baseURL:'https://api.sampleapis.com/coffee/hot',
      coffeeArray:[],
      isLoaded : false
    }
  },
  components: {
    CoffeeComp,
    LoaderComp
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
    }
  }
}
</script>

<style lang="scss">
@import './assets/style/general'

</style>
