<script lang="ts">
import MensagemLivros  from "@/components/MensagemLivros.vue";
import CaixaDialogo from "@/components/CaixaDialogo.vue";

//Fonte de dados arquivo Json.
import MensagensDataSource from '@/assets/json/mensagensDataSource.json' ;
import MensagensDialogoDataSource from '@/assets/json/mensagensDialogoDataSource.json';
export default {
  name: 'CaixaMensagem' ,
  data() {
    return {
      dialogoDataSource: MensagensDialogoDataSource,
      dialogo :[],
      mensagensDataSource : MensagensDataSource,
      showCaixaMensagemBody: false, 
      showCaixaDialogo: false,
      meuperfil_id: null, 
      livros_id:null, 
    }
  },
  components: {
    MensagemLivros, 
    CaixaDialogo,
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
    childFecharCaixaDialogo(valorHerdado) {
      this.showCaixaDialogo = valorHerdado;
    }
  }
}

</script>
<template>
  <h1>caixaMensagem</h1>
  {{ mensagensDataSource }}
  <div :class="{'row row-cols-2' : showCaixaDialogo , '':!showCaixaDialogo }">
    <div :class="{'col':showCaixaDialogo , '':!showCaixaDialogo}">
      <div class="caixaMensagem border border-secondary rounded" >
          <div class="caixaMensagemHeader" v-on:click="showCaixaMensagemBody=showCaixaMensagemBody===false">
          </div>
              <div class="caixaMensagemBody" :class="{ hide : showCaixaMensagemBody}">
              
                <div  v-for="mensagem in mensagensDataSource" class="border border-secondary">
                    <MensagemLivros :mensagem="mensagem" v-on:click="abrirDialogo( mensagem.meuperfil_id , mensagem.livros_id )" ></MensagemLivros>
                </div>
          </div>
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
