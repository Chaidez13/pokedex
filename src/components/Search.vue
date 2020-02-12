<template>
    <v-container class="red bor-red">
        <input type="text" v-model="pokemon" class="white bor-red all-wh">

        <router-link :to="{name: 'Pokedex' , params: {id:pokemon}}"><v-btn small>Buscar</v-btn></router-link>
    </v-container>
</template>

<script>
export default {
    data(){
        return{
            pokemon: ''
        }
    }
}
</script>
  
<style>
.bor-red{
    border-radius: 20px
}
.all-wh{
    width: 100%;
    padding: 3px 6px;
    margin-bottom: 10px;
}
</style>