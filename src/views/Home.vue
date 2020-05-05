<template>
  <div class="home">
    <header class="bg-header">
      <div class="center-img">
        <img src="../assets/images/Logo.png" alt="Logo Pastel de Ideias" />
      </div>
    </header>
    <section class="register">
      <img class="float-pastel-r z-5" src="../assets/images/pasteis-img.png" alt="Pastel" />
      <form @submit.prevent="sendInfo()" id="myForm" class="form relative z-15" name="Form">
        <div class="form-header">
          <p>Monte aqui o seu cardápio. O que está esperando?</p>
        </div>
        <div class="form-body relative z-20">
          <div class="row">
            <div class="col-40">
              <div class="ui-input">
                <input id="titulo" placeholder="Titulo do pedido" maxlength="60" minLength="3" required v-model="item.titulo" type="text" />
              </div>
            </div>
            <div class="col-40">
              <div class="ui-input">
                <input id="sabor" placeholder="Sabor"  maxlength="60" minLength="3" required v-model="item.sabor" type="text" />
              </div>
            </div>
            <div class="col-20">
              <div class="ui-input">
                <input id="valor" placeholder="R$" required v-model="item.valor" step="any" type="number" />
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col">
              <div class="ui-input">
                <textarea id="descricao" placeholder="Descrição" type="text" required v-model="item.descricao" rows="5"></textarea>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col">
              <div
                class="ui-upload d-flex justify-content-center flex-column align-items-center relative"
              >
                <input v-if="url == null"
                  @change="captureImg($event)"
                  class="send-img"
                  type="file"
                  id="sendImg"
                  name="img"
                  accept="image/*"
                  required
                />
                <div v-if="url" class="img-prev">
                 <!--<img width='180' height='180' :src="url" />-->
                <div class="float-img" :style="{'background-image': 'url('+ url + ')'}"></div>
                <div class="aling-info">
                <p>{{ item.image.name }}</p>
                <button type="button" @click="url = null">Excluir</button>
                </div>
                </div>
                <img
                  src="../assets/images/upload-icon.png"
                  width="48"
                  height="45"
                  alt="Icone envio de arquivo"
                  v-if="url == null"
                />
                <p v-if="url == null">Jogue aqui o arquivo de imagem do seu pastel ou clique para localizar a pasta.</p>
              </div>
            </div>
          </div>
        </div>
        <div class="row-btn">
          <button type="button" class="btn btn-red" v-on:click="clearFields()">Limpar</button>
          <button class="btn btn-yellow">Cadastrar</button>
        </div>
      </form>
    </section>
    <div class="line relative">
      <p>Veja como será apresentado ao cliente</p>
    </div>
    <section class="container">
      <base-item v-for="(item) in items" :item="item" :key="item" />
    </section>
  </div>
</template>

<script>
import BaseItem from '@/components/BaseItem.vue'

export default {
  name: 'Home',
  data: () => {
    return {
      item: {
        titulo: '',
        sabor: '',
        valor: '',
        descricao: '',
        image: ''
      },
      items: [],
      url: null
    }
  },
  created () {
    this.getData()
  },
  computed: {
    fileName () {
      const { image } = this.item
      if (image) {
        const split =
        image.name.split('.')
        return `${split[0]}-${new Date().getTime()}.${split[1]}`
      } else {
        return ''
      }
    }
  },
  components: {
    BaseItem
  },
  methods: {
    captureImg ({ target }) {
      this.item.image = target.files[0]
      this.url = URL.createObjectURL(this.item.image)
    },
    async sendInfo () {
      try {
        const ref = this.$firebase.database().ref(window.uid)
        const id = ref.push().key
        const picture = await this.$firebase
          .storage()
          .ref(window.uid)
          .child(this.fileName)
          .put(this.item.image)
        const url = await picture.ref.getDownloadURL()
        const item = {
          id,
          ...this.item,
          image: url,
          createdAt: new Date().getTime()
        }
        ref.child(id).set(item, err => {
          if (err) {
            console.error(err)
          } else {
            this.clearFields()
          }
        })
      } catch (err) {
        console.error(err)
      }
    },
    clearFields () {
      this.item.titulo = ''
      this.item.sabor = ''
      this.item.valor = ''
      this.item.descricao = ''
      this.url = null
    },
    getData () {
      const ref = this.$firebase.database().ref()
      ref.on('value', data => {
        const values = data.val()
        this.items = Object.keys(values).map(i => values[i])
      })
    }
  }
}
</script>

<style lang="scss">
  .img-prev{
    position: relative;
    z-index: 5;
    display: flex;
    flex-direction: column;
    align-items: center;
    .aling-info{
      display: flex;
      align-items: center;
    }
    p{
      margin: 15px 0px;
    }
    button{
      color: white;
      background: #E43636;
      border: none;
      box-shadow: none;
      border-radius: 20px;
      font-weight: bold;
      padding: 5px 10px;
      cursor: pointer;
      margin-left: 15px;
    }
  }
</style>
