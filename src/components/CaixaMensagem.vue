<script lang="ts">
import MensagemLivros  from "@/components/MensagemLivros.vue";
import CaixaDialogo from "@/components/CaixaDialogo.vue";

//Fonte de dados arquivo Json.
import MensagensDataSource from '@/assets/json/mensagensDataSource.json' ;

export default {
  name: 'CaixaMensagem' ,
  data() {
    return {
      mensagensDataSource : MensagensDataSource,
      showCaixaMensagemBody : false
    }
  },
  components: {
    MensagemLivros, 
    CaixaDialogo,
  }
}
console.log(MensagensDataSource);

</script>
<template>
  <h1>caixaMensagem</h1>
  {{ mensagensDataSource }}
  <div class="caixaMensagem">
      <div class="caixaMensagemHeader" v-on:click="showCaixaMensagemBody=showCaixaMensagemBody===false">

      </div>
      <div class="caixaMensagemBody" :class="{ hideMensagemBody : showCaixaMensagemBody}">
        <div v-for="mensagem in mensagensDataSource">
          <MensagemLivros ></MensagemLivros>
        </div>
        

      </div>
      <CaixaDialogo></CaixaDialogo>
  </div>
    
</template>

<style scoped>
  .caixaMensagem{
    position: absolute;
    right: 0px ; 
    bottom: 0px;
  }
  .caixaMensagemHeader{
    height: 3em;
    min-width: 21em;
    max-width: 30em;
    background:red ;
    border:solid;
  }
  .caixaMensagemBody{
    min-height: 15em;
    max-height: 21em;
    min-width: 21em;
    max-width: 30em;
    background:red ;
    border:solid;
    scroll-behavior: auto;
  }
  .hideMensagemBody{
    display: none;
  }
</style>
