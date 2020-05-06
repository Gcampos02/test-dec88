<template>
  <div class="base-spinner fa-3x" v-if="!visible" >
  <img src="../../assets/images/mas-logo.png" width="150" height="137" class="flip" alt="Mascote"/>
  <p>Carregando ...</p>
  </div>
</template>

<script>
export default {
  data () {
    return {
      visible: true
    }
  },
  created () {
    this.$root.$on('Spinner::show', () => { this.visible = true })
    this.$root.$on('Spinner::hide', () => { this.visible = false })
  },
  methods: {
    alterarSpinner () {
      this.visible = !this.visible
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/scss/_color";

@keyframes spin
{
  100% { transform: rotateY(360deg); }
}

.base-spinner{
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  position: fixed;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: $red-001;
  color: $white;
  overflow-y: hidden;
  z-index: 30;
  p{
    color: $white;
    font-size: 24px;
    font-style: italic;
    font-weight: bold;
    margin-top: 20px;
  }
}

.flip{
  -webkit-animation:spin 2500ms linear infinite;
  animation: spin 2500ms linear infinite;
  transform-style: preserve-3d;
}

</style>
