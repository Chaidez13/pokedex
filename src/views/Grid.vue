<template>
  <v-container>
      <v-row>
          <v-col>
              <v-card>
                  <v-date-picker 
                  v-model="fecha"
                  full-width
                  locale="es-mx"
                  :min="minimo"
                  :max="maximo"
                  @change="getDolar(fecha)">
                  </v-date-picker>
              </v-card>
              <v-card color="primary" dark> 
                  <v-card-text class="display-1 text-center">
                      {{valor}} 
                  </v-card-text>
              </v-card>
          </v-col>
      </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
import { mapMutations } from 'vuex'

export default {
    data(){
        return {
            fecha: new Date().toISOString().substr(0, 10),
            minimo: '1999',
            maximo: new Date().toISOString().substr(0, 10),
            valor: null
        }
    },
    methods: {
        ...mapMutations(['mostrarLoading','ocultarLoading']),

        async getDolar(dia){
            let inverter = dia.split('-').reverse().join('-')

            try {
                this.mostrarLoading({titulo:'Accediendo a Información', color:'secondary'})

                let datos = await axios.get(`https://mindicador.cl/api/dolar/${inverter}`)
                //console.log(datos)
                this.valor = await datos.data.serie[0].valor
            } catch (error) {
                console.log(error)
            }
            finally{
                this.ocultarLoading()
            }
        }
    },
    created(){
        this.getDolar(this.fecha)
    }
}
</script>
<!-- 

<v-row>
          <v-col cols="12" sm="6">
              <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolorum, ipsam ea! Sit at distinctio fugit tempore adipisci, magnam, 
                  iusto provident voluptate, minus vero deleniti quo tenetur dolorem laudantium totam. Odio?</p>
          </v-col>
          <v-col cols="12" sm="6">
              <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolorum, ipsam ea! Sit at distinctio fugit tempore adipisci, magnam, 
                  iusto provident voluptate, minus vero deleniti quo tenetur dolorem laudantium totam. Odio?</p>
          </v-col>
      </v-row>

-->