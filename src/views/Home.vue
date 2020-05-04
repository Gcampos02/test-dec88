<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <header class="bg-header">
        <div class="center-img">
            <img src="../assets/images/Logo.png" alt="Logo Pastel de Ideias">
        </div>
    </header>
    <section class="register">
      <img class="float-pastel-r z-5" src="../assets/images/pasteis-img.png" alt="Pastel">
        <div id="myForm" class="form relative z-15" name="Form">
          <div class="form-header">
            <p>Monte aqui o seu cardápio. O que está esperando?</p>
          </div>
          <div class="form-body relative z-20">
            <div class="row">
              <div class="col-40">
                  <div class="ui-input">
                      <input id="titulo" placeholder="Titulo do pedido" type="text">
                  </div>
              </div>
              <div class="col-40">
                  <div class="ui-input">
                      <input id="sabor" placeholder="Sabor" type="text">
                  </div>
              </div>
              <div class="col-20">
                  <div class="ui-input">
                      <input id="valor" placeholder="R$"  type="number">
                  </div>
              </div>
            </div>
            <div class="row">
                  <div class="col">
                      <div class="ui-input">
                          <textarea id="descricao" placeholder="Descrição" rows="5"></textarea>
                      </div>
                  </div>
            </div>
            <div class="row">
                <div class="col">
                    <div class="ui-upload d-flex justify-content-center flex-column align-items-center relative">
                        <input class="send-img" type="file" id="sendImg" name="img"
                            accept="image/*">
                        <img src="../assets/images/upload-icon.png" width="48" height="45" alt="Icone envio de arquivo">
                        <p>Jogue aqui o arquivo de imagem do seu pastel ou clique para localizar a pasta.</p>
                    </div>
                </div>
            </div>
          </div>
          <div class="row-btn">
              <button class="btn btn-red" v-on:click="clearFields()">
                  Limpar
              </button>
              <button class="btn btn-yellow" v-on:click="sendInfo()">
                  Cadastrar
              </button>
          </div>
        </div>
    </section>
    <div class="line relative">
        <p>Veja como será apresentado ao cliente</p>
    </div>
    <section class="container">
      <!-- <div v-if="isItem" v-for="item in listItem.contracts"> -->
        <base-item/>
      <!-- </div> -->
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import BaseItem from '@/components/BaseItem.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld
    BaseItem
  }
}
</script>
