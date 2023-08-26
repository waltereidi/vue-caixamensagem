<script lang="ts">
import config from "@/assets/json/bibliotecaconfig.json";
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
        
    },
    data() {
        return {
            configDataSource: config, 
        }
    },
    emits: ['deletarMensagem'],
}

</script>

<template>

    <div class="card">
      <div class="card-body">
        <div class="card-subtitle mb-2 text-muted" id="dialogoHeader">
            <table >
                <tr>
                    <th class="tableHeader1">
                        <a :href="'meuperfil/'+this.mensagem.meuperfil_id">
                            <img class="profile_picture rounded-circle" :src="this.configDataSource.profile_pictureDefault">
                        </a>
                    </th>
                    <th class="tableHeader2"><h6>{{ this.mensagem.created_at }}</h6></th>
                    <th class="tableHeader3"></th>
                    <th class="tableHeader4" v-if="this.meuperfil_id == this.mensagem.meuperfil_id"><i class="bi bi-trash" v-on:click="deletarMensagem(this.mensagem.id)"></i></th>
                </tr>
            </table>
            
        </div>
          <p class="card-text"> {{ this.mensagem.mensagem }}</p>
        </div>
    </div>
</template>

<style scoped>
@import "@/css/CaixaMensagem/dialogoMensagem.css";
</style>