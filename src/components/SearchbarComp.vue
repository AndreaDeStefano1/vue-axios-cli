<template>
  <div class="row my-5">

    <div class="col-10">
      <input @keyup.enter="$emit('search', coffeeSearch)" v-model.trim="coffeeSearch" class='form-control' type="text">
    </div>

    <div class="col">
      <button @click="$emit('search', coffeeSearch)" class="btn btn-info">Cerca</button>
    </div>
    <div class="col">
      <button @click="resetFunction" class="btn btn-warning">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchbarComp',
  data(){
    return{
      coffeeSearch: '',
    }
  },
  methods:{
    resetFunction(){
      this.coffeeSearch = '';
      this.$emit('search', '');
    },
  },
}
</script>

<style>

</style>