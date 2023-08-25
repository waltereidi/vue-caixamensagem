<script lang="ts">
import MensagemLivros  from "@/components/MensagemLivros.vue";
import CaixaDialogo from "@/components/CaixaDialogo.vue";
import ListaAmigos from "@/components/ListaAmigos.vue";

//Fonte de dados arquivo Json.
import MensagensDataSource from '@/assets/json/mensagensDataSource.json' ;
import MensagensDialogoDataSource from '@/assets/json/mensagensDialogoDataSource.json';
import listaAmigosDataSource from "@/assets/json/listaamigos.json";
export default {
  name: 'CaixaMensagem' ,
  data() {
    return {
      dialogoDataSource: MensagensDialogoDataSource,
      dialogo :[],
      mensagensDataSource: MensagensDataSource,
      listaAmigosDataSource: listaAmigosDataSource,
      showCaixaMensagemBody: false, 
      showCaixaDialogo: false,
      meuperfil_id: null, 
      livros_id: null, 
      caixaMensagemAmigos: false,
    }
  },
  components: {
    MensagemLivros, 
    CaixaDialogo,
    ListaAmigos,
  }, 
  methods:{
    abrirDialogo(meuperfil_id, livros_id) {
      this.showCaixaDialogo = true;
      this.meuperfil_id = meuperfil_id;
      this.livros_id = livros_id;

      let novoDialogo =[]; 
      this.dialogoDataSource.forEach((value, index) => {
        if (value.livros_id === this.livros_id && value.meuperfil_id === this.meuperfil_id) {
          novoDialogo.push(value);
        }
      });
      this.dialogo = novoDialogo; 
    },
    childFecharCaixaDialogo() {
      this.showCaixaDialogo = false;
    }, 
    childDeletarAmigo(id) {
      if (confirm('Deseja realmente deletar este amigo?')) {
        const amigoIndex = this.listaAmigosDataSource.findIndex(value => value.id === id);
        this.listaAmigosDataSource.splice(amigoIndex, 1);
      }
    }
  }
}

</script>
<template>
  <h1>caixaMensagem</h1>
  <div :class="{'row row-cols-2' : showCaixaDialogo , '':!showCaixaDialogo }">
    <div :class="{'col':showCaixaDialogo , '':!showCaixaDialogo}">
      <div class="caixaMensagem border border-secondary rounded" >
          <div class="caixaMensagemHeader" v-on:click="showCaixaMensagemBody=showCaixaMensagemBody===false">
              <h6>Mensagens</h6>
          </div>

          <div class="caixaMensagemBody" :class="{ hide : showCaixaMensagemBody }">
              <table v-if="!caixaMensagemAmigos">
                  <div id="caixaMensagemBodyCard" v-for="mensagem in mensagensDataSource" class="border" v-on:click="abrirDialogo(mensagem.meuperfil_id, mensagem.livros_id)" >
                      <MensagemLivros :mensagem="mensagem"></MensagemLivros>
                  </div>
              </table>

              <table v-if="caixaMensagemAmigos">
                    <div id="caixaMensagemBodyCard" v-for="amigo in listaAmigosDataSource" class="border" >
                        <ListaAmigos :amigo="amigo" @deletarAmigo="childDeletarAmigo"></ListaAmigos>
                    </div>
              </table>
          </div>
          <ul class="nav nav-tabs">
              <li class="nav-item">
                <a :class="{'nav-link active':!caixaMensagemAmigos , 'nav-link' : caixaMensagemAmigos }" v-on:click="caixaMensagemAmigos=false" aria-current="page" href="#">Mensagens</a>
              </li>
              <li class="nav-item">
                <a :class="{ 'nav-link active': caixaMensagemAmigos, 'nav-link': !caixaMensagemAmigos }" v-on:click="caixaMensagemAmigos=true" href="#">Lista de amigos</a>
              </li>
          </ul>
      </div>
    </div>
    <div :class="{'col' : showCaixaDialogo , 'hide' : !showCaixaDialogo}">
        <div class="caixaDialogo border border-secondary rounded" >
           <CaixaDialogo :dialogo="this.dialogo" :meuperfil_id="this.meuperfil_id" :livros_id="this.livros_id" @fecharCaixaDialogo="childFecharCaixaDialogo"></CaixaDialogo>
        </div>
    </div>
  </div>  

</template>

<style scoped>
@import '@/css/CaixaMensagem/caixaMensagem.css';  
</style>
