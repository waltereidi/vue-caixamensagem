<script lang="ts">
import DialogoMensagem from "@/components/DialogoMensagem.vue";

export default {
    props: {
        dialogo: Object, 
        meuperfil_id: Number, 
        livros_id: Number , 
    }, 
    data() {
        return {
            enviarMensagemInput: null,
            showCaixaDialogo: true,
        }
    },
    components: {
        DialogoMensagem,
    },
    methods: {
        enviarMensagem() {
            const dados = {
                "meuperfil_id": this.meuperfil_id,
                "livros_id": this.livros_id,
                "mensagem": this.enviarMensagemInput,
            }
            this.dialogo.push(dados);
        },
        fecharCaixaDialogo() {
            this.$emit('fecharCaixaDialogo', false);
        },
        childDeletarMensagem(valorHerdado) {
            const index = this.dialogo.findIndex(value => value.id === valorHerdado);
            this.dialogo.splice(index, 1);
        }
    },
   
}
</script>
<template>
    <div class="caixaDialogoHeader border border-secondary" >
        <div class="row">
            <div class="col-10" v-on:click="showCaixaDialogo = showCaixaDialogo == false"></div>
            <div class="col-1"><i v-on:click="fecharCaixaDialogo" class="bi bi-x-square"></i></div>
            <div class="col-1"></div>
        </div>
    </div>

    <div :class="{'caixaDialogoBody border border-secondary' : showCaixaDialogo , 'hide' : !showCaixaDialogo }">
        <div class="row mensagemDialogo" v-for="mensagem in this.dialogo">
            <DialogoMensagem :mensagem="mensagem" :meuperfil_id="meuperfil_id" :livros_id="livros_id" @deletarMensagem="childDeletarMensagem"></DialogoMensagem>
            
        </div>
    </div>
    
    <div class="caixaDialogoFooter border border-secondary">
        <div class="input-group mb-3">
            <input type="text" class="form-control" placeholder="Recipient's username" aria-label="Recipient's username" aria-describedby="basic-addon2"
                v-model="this.enviarMensagemInput">
            <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" v-on:click="enviarMensagem">Enviar</button>
            </div>
        </div>
    </div>
    
</template>
<style>
    @import "@/css/CaixaMensagem/caixaDialogo.css";
</style>