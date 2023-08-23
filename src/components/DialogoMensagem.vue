<script lang="ts">
export default {
    props: {
        mensagem: Object,
        meuperfil_id: Number,
        livros_id: Number,
    },
    methods:{
        deletarMensagem(id) {
            if(confirm("deseja deletar esta mensagem?"))
            {
                this.$emit('deletarMensagem', id);
            }
        }
        
    }
}

</script>

<template>
    <div class="row mensagemDialogo">
        <div class="col-2"> <p class="text-sm-start text-break">{{ this.mensagem.id }}</p> </div>
        <div class="col-9"> <p class="text-sm-start text-break">{{ this.mensagem.mensagem }}</p> </div>
        <div class="col-1"><i class="bi bi-x-square" v-on:click="deletarMensagem(this.mensagem.id)"></i> </div>
    </div>
    
</template>

<style scoped>
@import "@/css/CaixaMensagem/dialogoMensagem.css";
</style>