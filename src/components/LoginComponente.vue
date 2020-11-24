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
    ></v-text-field>
    </v-card-text>

    <v-card-text>
    <v-text-field
      label="Contraseña"
      :rules="rules"
      hide-details="auto"
    ></v-text-field>
    </v-card-text>

    <v-card-actions>
      <v-btn
        text
        color="teal accent-4"
      >
        Iniciar sesion
      </v-btn>
    </v-card-actions>
  </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component({
  components: {
  },
  data: ()=>({
      rules: [
        value => !!value || 'Requerido.',
        value => (value && value.length >= 3) || 'Min 3 caracteres',
      ],
  })
})
export default class LoginComponente extends Vue {}
</script>
