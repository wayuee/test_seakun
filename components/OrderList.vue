<template>
  <div class="pt-2 pl-52">
      <div class="mr-10 -mt-10">
      <CardOrder :card-order="dataOrder"/>
      </div>
    </div>
</template>

<script>
import CardOrder from "~/components/CardOrder"
export default {
  components:{
    CardOrder,
  },
  props:{
    dataOrder:{
      type:Object,
      default:{},
    }
  }
}
</script>

<style>

</style>