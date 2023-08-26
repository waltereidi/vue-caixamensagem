<script lang="ts">
import DialogoMensagem from "@/components/DialogoMensagem.vue";
import CaixaDialogoFooter from "@/components/CaixaDialogoFooter.vue";

export default {
    props: {
        dialogo: Object, 
        meuperfil_id: Number, 
        livros_id: Number, 
        user:Object,
    }, 
    data() {
        return {
            enviarMensagemInput: "",
            showCaixaDialogo: true,
        }
    },
    components: {
        DialogoMensagem,
        CaixaDialogoFooter,
    },
    methods: {
        childEnviarMensagem(enviarMensagemInput:string , linkLivroInput:string ) {
            const dados:object = {
                "meuperfil_id": this.meuperfil_id,
                "livros_id": this.livros_id,
                "mensagem": enviarMensagemInput,
                "linkLivroInput": linkLivroInput , 
            }
            this.dialogo.push(dados);
        },
        fecharCaixaDialogo() {
            this.$emit('fecharCaixaDialogo');
        },
        childDeletarMensagem(valorHerdado:number ) {
            const index = this.dialogo.findIndex(value => value.id === valorHerdado);
            this.dialogo.splice(index, 1);
        }
    },
    emits: ['fecharCaixaDialogo']
}
</script>
<template>
    <div class="caixaDialogoHeader" >
         <div class="container">
            <div class="row">
                <div class="col-sm"><a :href="meuperfil_id">UserName</a></div>

                <div v-on:click="showCaixaDialogo = showCaixaDialogo == false" class="col"></div>
                <div v-on:click="showCaixaDialogo = showCaixaDialogo == false" class="col"></div>

                <div class="col">
                     <i v-on:click="showCaixaDialogo = showCaixaDialogo == false" :class="{ 'bi bi-dash-square': showCaixaDialogo, 'bi bi-window': !showCaixaDialogo }" ></i>
                     <i  v-on:click="fecharCaixaDialogo" class="bi bi-x-square-fill text-danger m-3"></i>
                </div>
                
            </div>
    </div>
    </div>

    <div :class="{'caixaDialogoBody' : showCaixaDialogo , 'hide' : !showCaixaDialogo }">
        <div class="row mensagemDialogo" v-for="mensagem in this.dialogo">
            <DialogoMensagem :mensagem="mensagem" :meuperfil_id="meuperfil_id" :livros_id="livros_id" @deletarMensagem="childDeletarMensagem"></DialogoMensagem>
            
        </div>
    </div>
    
        <CaixaDialogoFooter :showCaixaDialogo="showCaixaDialogo" :linkLivro="true" @enviarMensagem="childEnviarMensagem"></CaixaDialogoFooter>
    
</template>
<style>
    @import "@/css/CaixaMensagem/caixaDialogo.css";
</style>