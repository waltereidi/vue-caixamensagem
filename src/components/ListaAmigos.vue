<script lang="ts">
import config from "@/assets/json/bibliotecaconfig.json";
export default { 
    props: {
            amigo:Object
    },
    data() {
        return {
            configDataSource: config, 
                
            }
        },
    methods: {
        
        deletarAmigo(id) {
           
                this.$emit('deletarAmigo', id);
            
        }
    },
    emits: ['deletarAmigo'],
    }
</script>
<template>
    <tr>
        <td class="listaAmigoTd1"><a :href="'/meuperfil/'+amigo.meuperfil_id "><img :src="amigo.profile_picture??configDataSource.profile_pictureDefault"></a></td>
        <td class="listaAmigoTd2"> <p>{{ amigo.nome }}</p></td>
        <td class="listaAmigoTd3"> <p>{{ amigo.ultimologin }}</p></td>
        <td class="listaAmigoTd4">
            <div class="options">
               <i class="bi bi-person-dash-fill text-danger m-3" v-on:click="deletarAmigo(amigo.id)"></i>
            </div>
        </td>
            
      
    </tr>
</template>
<style scoped>
    @import "@/css/CaixaMensagem/listaamigos.css";
</style>