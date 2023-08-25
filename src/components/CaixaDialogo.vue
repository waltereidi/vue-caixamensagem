<script lang="ts">
import DialogoMensagem from "@/components/DialogoMensagem.vue";

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
            this.$emit('fecharCaixaDialogo');
        },
        childDeletarMensagem(valorHerdado) {
            const index = this.dialogo.findIndex(value => value.id === valorHerdado);
            this.dialogo.splice(index, 1);
        }
    },
    emits: ['fecharCaixaDialogo']
}
</script>
<template>
    <div class="caixaDialogoHeader" >
        <div class="row">
            <div class="col-9" v-on:click="showCaixaDialogo = showCaixaDialogo == false"><a :href="meuperfil_id">UserName</a></div>
            <div class="col-1"  id="botoesHeader">
                <i v-on:click="showCaixaDialogo = showCaixaDialogo == false" :class="{'bi bi-dash-square ': showCaixaDialogo , 'bi bi-window' :!showCaixaDialogo}" ></i>
            </div>
            <div class="col-1"  id="botoesHeader">
                  <i v-on:click="fecharCaixaDialogo" class="bi bi-x-square">x</i>
                </div>
            <div class="col-1"></div>
        </div>
    </div>

    <div :class="{'caixaDialogoBody' : showCaixaDialogo , 'hide' : !showCaixaDialogo }">
        <div class="row mensagemDialogo" v-for="mensagem in this.dialogo">
            <DialogoMensagem :mensagem="mensagem" :meuperfil_id="meuperfil_id" :livros_id="livros_id" @deletarMensagem="childDeletarMensagem"></DialogoMensagem>
            
        </div>
    </div>
    
    <div class="caixaDialogoFooter">
        <div class="input-group input-group-sm mb-3">
              <textarea class="form-control" placeholder="Digite algo..." aria-label="Digite algo..." v-model="enviarMensagemInput" aria-describedby="botao-addon" rows="1"></textarea>
              <button class="btn btn-primary" :disabled="this.enviarMensagemInput.length==0" type="button" id="botao-addon" v-on:click="enviarMensagem">Enviar</button>
            </div>
    </div>
    
</template>
<style>
    @import "@/css/CaixaMensagem/caixaDialogo.css";
</style>