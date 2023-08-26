<script lang="ts">

export default { 
    props: {
        showCaixaDialogo: Boolean, 
        linkLivro : Boolean ,
        
    },
    data() {
        return {
            enviarMensagemInput: '',
            linkLivroInput:'',      
        }
    },
    emits: ['enviarMensagem'],
    methods:{
        enviarMensagem(){
            this.$emit('enviarMensagem' , this.enviarMensagemInput , this.linkLivroInput);
        }            
    }
        
    }
</script>
<template>
    <div :class="{'caixaDialogoFooter':showCaixaDialogo , 'hide':!showCaixaDialogo}" >
        
        <label :class="{'hide' :!linkLivro}" for="basic-url">Link do livro</label>   
        <div :class="{'input-group mb-3' : linkLivro , 'hide':!linkLivro}">
            <input v-model="linkLivroInput" type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3">
        </div>
            <div class="input-group input-group-sm mb-3">
                  <textarea class="form-control" placeholder="Digite algo..." aria-label="Digite algo..." v-model="enviarMensagemInput" aria-describedby="botao-addon" rows="1"></textarea>
                  <button class="btn btn-primary" :disabled="enviarMensagemInput.length == 0" type="button" id="botao-addon" v-on:click="enviarMensagem">Enviar</button>
                </div>
        </div>
</template>