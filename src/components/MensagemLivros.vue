<script>
import bibliotecaconfig from "@/assets/json/bibliotecaconfig.json";

export default {
    props: {
        mensagem: Object,
    },
    data() {
        return {
            capaDefault: bibliotecaconfig.profile_pictureDefault, 
             
        }
    }
    }
</script>
<template>
            <tr class="mensagensLivrosTableRow1">
                <td class="mensagensLivrosTdCol1" rowspan="2"><img :src="this.capaDefault" class="rounded-circle" ></td>
                <td class="mensagensLivrosTdCol2" rowspan="2">{{ this.mensagem.livro_titulo }}</td>
                <td class="mensagensLivrosTdCol3">{{ this.mensagem.autores_nome }} </td>
                <td class="mensagensLivrosTdCol4" rowspan="2"><i :class="{'bi bi-circle text-danger m-3' : !this.mensagem.visualizado, 'bi bi-check2-all text-primary m-3': this.mensagem.visualizado}"></i></td>
            </tr>
            <tr class="mensagensLivrosTableRow2">
                <td class="mensagensLivrosTdCol3">{{ this.mensagem.editoras_nome }}</td>
            </tr>
       
</template>
<style scoped>
@import "@/css/CaixaMensagem/mensagemLivros.css";

</style>