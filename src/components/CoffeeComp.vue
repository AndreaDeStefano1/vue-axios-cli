<template>
  <div class="">
    <h3>{{coffeItem.title}}</h3>
    <p>{{coffeItem.description}}</p>
    <ul>
      <h4>Ingredienti:</h4>
      <li v-for="(ingredient,index) in coffeItem.ingredients" :key="`ingredient-${index}`">{{ingredient}} </li>
     
    </ul>
  </div>
</template>

<script>
export default {
  name: 'CoffeeComp',
  props:{
    coffeItem : Object
  }
}

</script>

<style>

</style>