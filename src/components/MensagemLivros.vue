<script>
import bibliotecaconfig from "@/assets/json/bibliotecaconfig.json";

export default {
    props: {
        mensagem: Object,
    },
    data() {
        return {
            capaDefault: bibliotecaconfig.capaLivroDefault, 
             
        }
    }
    }
</script>
<template>

   <div class="container text-center" id="container">
        <div class="row row-cols-4">
            <div class="col">
                <img :src="this.capaDefault" class="mg-fluid img-thumbnail">
            </div>
            <div class="col">
                <p class="text-sm-start text-break" >{{ this.mensagem.livro_titulo }}</p>
            </div>
            <div class="col">
                    <div class="row">
                        <p class="text-sm-start " >{{ this.mensagem.autores_nome }}</p>
                    </div>
                    <div class="row">
                         <p class="text-sm-start " >{{ this.mensagem.editoras_nome }}</p>
                    </div>
            </div>
            <div class="col"> 
                <i :class="{'bi bi-bookmark-check-fill fa-6x text-success m-3' : this.mensagem.visualizado}"></i>
            </div>
        </div>
   </div>

</template>
<style scoped>
 p {
    font-size: 0.8em;
 }

</style>