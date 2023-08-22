<script>
export default {
    props: {
        mensagem:Object
    }
    }
</script>
<template>
   <div class="container text-center">
        <div class="row">
            <div class="col-3">
                {{ this.mensagem.capalivro }}
            </div>
            <div class="col-3">
                {{ this.mensagem.livro_titulo }}
            </div>
            <div class="col-3">
                {{ this.mensagem.autores_nome }}
            </div>
            <div class="col-3"> 
                {{ this.mensagem.visualizado}}
            </div>
        </div>
   </div>
</template>
<style scoped>
    

</style>