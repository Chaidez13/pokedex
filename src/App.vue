<template>
  <v-app>
    <v-app-bar
      app
      color="red"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Pokedex Logo"
          class="shrink mr-2"
          contain
          src="@/assets/poke_logo.png"
          transition="scale-transition"
          width="40"
        />
      </div>
      <span class="title">Pokedex</span>
    </v-app-bar>

    <v-content>
      <v-container>
            <v-dialog
              v-model="loading.estado"
              hide-overlay
              persistent
              width="300">

              <v-card
                color="loading.color"
                dark>

                <v-card-text>
                  {{loading.titulo}}
                  <v-progress-linear
                    indeterminate
                    color="white"
                    class="mb-0"
                  ></v-progress-linear>

                </v-card-text>

              </v-card>

            </v-dialog>

        <router-view></router-view>
        
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import { mapState } from 'vuex';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),

  computed:{
    ...mapState(['loading'])
  }
};
</script>
