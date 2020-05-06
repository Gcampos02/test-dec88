<template>
  <div class="base-item" v-if="item.tipo == itemSelect">
      <div class="item">
          <div class="float-img float" :style="{'background-image': 'url(' + item.image + ')'}">
          </div>
          <div class="item-box">
              <div class="item-box-header">
                  <p class="title">{{item.titulo}}</p>
                  <p class="value" v-money-format='item.valor'></p>
              </div>
              <div class="item-box-body">
                   <p>Sabor: <span>{{item.sabor}}</span></p>
                  <p>Descrição: <span>{{item.descricao}}</span></p>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'BaseItem',
  props: {
    item: { type: Object, required: true },
    itemSelect: { type: String, required: true }
  }
}
</script>

<style scoped lang="scss">

</style>
