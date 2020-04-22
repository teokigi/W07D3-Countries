<template lang="">
  <div>
    <p><img v-bind:src="country.flag"></p>
    <p>{{country.name}}</p>
    <p> {{country.borders}}</p>
  </div>
</template>

<script>
export default {
  name:'countries-list',
  props:['country']
}
</script>

<style lang="css" scoped>
img{
  width:100px;
}
</style>
