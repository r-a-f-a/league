<template>
  <div>
    <card :champion="$route.params.id"></card>
  </div>
</template>

<script>
import card from './comps/card'
export default {
components:{
  card
}
}
</script>

<style>

</style>