<template>
  <div id="app" class="bg-body">
    <router-view/>
    <base-spinner/>
  </div>
</template>

<script>
import BaseSpinner from '@/components/global/BaseSpinner.vue'
export default {
  name: 'App',
  components: {
    BaseSpinner
  }
}
</script>

<style lang="scss">

</style>
