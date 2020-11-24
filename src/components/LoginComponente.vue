<template>
  <div class="loginComponente">
    <v-card
    class="mx-auto"
    max-width="344"
    elevation="24"
    tile
    >
    <v-card-text>
      <!-- <div>Word of the Day</div> -->
      <p class="display-1 text--primary">
        Login
      </p>
    </v-card-text>

    <v-card-text>
    <v-text-field
      label="Usuario"
      :rules="rules"
      hide-details="auto"
      v-model="user"
      append-icon="mdi-account"
    ></v-text-field>
    </v-card-text>

    <v-card-text>
    <v-text-field
      label="Contraseña"
      :rules="rules"
      hide-details="auto"
      v-model="password"
      :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
      :type="show ? 'text' : 'password'"
      class="input-group--focused"
      @click:append="show = !show"

    ></v-text-field>
    </v-card-text>

    <v-card-actions>
      <v-btn
        text
        color="teal accent-4"
        v-on:click="submit()"
      >
        Iniciar sesion
      </v-btn>
    </v-card-actions>
  </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Router from 'vue-router'
@Component({
  components: {
  },
  data: ()=>({
      rules: [
        value => !!value || 'Requerido.',
        value => (value && value.length >= 3) || 'Min 3 caracteres',
      ],
      user:"",
      password:"",
      show:false,
        submit:function(){
            this.user="presione el boton"
            this.$router.push('/admin')
            
        }
  }),
  
})
export default class LoginComponente extends Vue {}
</script>
