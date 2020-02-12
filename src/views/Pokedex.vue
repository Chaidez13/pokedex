<template>
    <v-container class="red">
        <v-row>
            <v-col cols="6">
                {{namePkm}}
                <v-img :src="imgPkm"></v-img>
            </v-col>
            <v-col cols="6">
                HOLA
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import axios from 'axios'
import {mapMutations} from 'vuex'

export default {
    data(){
        return{
            namePkm: '',
            imgPkm: ''
            // ,datosPkm: null 
        }
    },
    methods:{
        ...mapMutations(['mostrarLoading','ocultarLoading']),
        async getData(pokeId){
            try {
                this.mostrarLoading({titulo:'Consiguiendo Datos', color:'red'})
                let datos = await axios.get(`https://pokeapi.co/api/v2/pokemon/${pokeId}`)
                console.log(datos)
                //this.datosPkm = await datos
                //this.valor = await datos.data.serie[0].valor
                this.namePkm = datos.data.name.charAt(0).toUpperCase() + datos.data.name.slice(1);
                console.log(datos.data.moves[0].move)
                this.imgPkm = datos.data.sprites.front_default
            } catch (error) {
                console.log(error)
            }
            finally{
                this.ocultarLoading()
            }
        }
    },
    created(){
        this.getData(this.$route.params.id)
    }
}


//https://pokeapi.co/api/v2/pokemon/   803 el último
</script>

<style scoped>

</style>

