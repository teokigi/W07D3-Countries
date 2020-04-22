<template lang="html">
  <div id="favlist">
    <p><img v-bind:src="country.flag"> {{country.name}}</p>
  </div>
</template>

<script>
export default {
  name:'favourite-countries-list',
  props:['country']
}
</script>

<style lang="css" scoped>
img{
  width:100px;
}
#favlist{
  border-style:solid;
}
</style>
