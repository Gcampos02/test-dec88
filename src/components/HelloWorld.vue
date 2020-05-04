<template>
  <div class="hello">

    <base-item/>
  </div>
</template>

<script>
import BaseItem from './BaseItem'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    BaseItem
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
