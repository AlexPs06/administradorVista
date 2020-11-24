<template>
  <v-app class="adminView" :style="{background: '#5d9b9b', }" >
  
   <v-container>
    <v-row justify="space-around">
      <v-col cols="12" md="4">
        <!-- <v-sheet
          class="pa-12"
          color="grey lighten-3"
          elevation="24"
        > -->
           <!-- overflow-y: auto; -->
            <!-- max-height="800" -->

        
        <v-list   >
            <v-subheader>Archivos</v-subheader>
            <v-list-item-group
            v-model="selectedItem"
            color="primary"
            style="max-height: 500px" class="overflow-y-auto"
            >
            <v-list-item
                v-for="(item, i) in items"
                :key="i"
            >
                <v-list-item-icon>
                <v-icon v-text="item.icon" ></v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                    <v-list-item-title v-text="item.text"></v-list-item-title>
                </v-list-item-content>
                
                
                <v-divider></v-divider>

            </v-list-item>

            </v-list-item-group>
        </v-list>

      </v-col>



      <v-col >
        <v-sheet
          class="pa-12"
          color="grey lighten-3"
          elevation="24"

        >

        </v-sheet>
        
      </v-col>


    </v-row>
  </v-container>


  </v-app>
</template>

<script lang="js">
import { Component, Vue } from 'vue-property-decorator';
// import * as fs from 'fs'
// import * as path from 'path'
// const fs = require('fs');
// const path = require('path');
// import * as fs from 'fs';

@Component({
  components: {
  },
  data: () => ({
      elevations: [6, 12, 18],
      selectedItem: 1,
      items: [
        { text: 'Real-Time', icon: 'mdi-pencil' },
        { text: 'Audience', icon: 'mdi-account' },
        { text: 'Conversions', icon: 'mdi-flag' },
        { text: 'Conversions', icon: 'mdi-flag' },
    
      ],
    }),
    beforeCreate(){

        // const RUTA_FOLDER = "C:\\Users\\luis_\\Documents\\Maestria\\inteligencia artificial\\CHATBOT-T\\api\\admin\\admin"
        // console.log(this.fs);
        // console.log(this.path);
        
        // fs.readdir(RUTA_FOLDER, function (err, archivos) {
        //     if (err) {
        //         console.log(err);
        //     return;
        //     }
        //     console.log(archivos);
        // });
    },
  
 
})
export default class AdminView extends Vue {}
</script>
