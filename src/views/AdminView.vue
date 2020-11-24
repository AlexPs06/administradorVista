<template>
  <v-app class="adminView" :style="{background: '#5d9b9b', }" >
    <v-container fill-height fluid>
        <v-row align="center"
            justify="center">
            <v-col>
                <Login/>
                
            </v-col>
        </v-row>
    </v-container>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Login from '../components/LoginComponente.vue';
@Component({
  components: {
      Login
  },
  
 
})
export default class AdminView extends Vue {}
</script>
