<template>
  <v-app class="adminView" :style="{background: '#5d9b9b', }" >
  
   <v-container>
    <v-row justify="space-around">
      <v-col cols="12" md="4">
        


  <v-card
    color="grey lighten-4"
    flat
    tile
    class="d-flex flex-wrap"
  >
    <v-toolbar dense>
      <!-- <v-app-bar-nav-icon></v-app-bar-nav-icon> esto falta checar si se queda o se va  -->

      <v-toolbar-title>Archivos</v-toolbar-title>
      <v-spacer></v-spacer>
        <!-- <v-text-field  label="Buscar"  hide-details="auto" v-model="search" clearable> </v-text-field> -->


      <v-icon>mdi-magnify</v-icon>
        <v-text-field  label="Buscar"  hide-details="auto" v-model="search" clearable> </v-text-field>




    </v-toolbar>
  </v-card>







      <UploadFileComponent   @clicked="onClickChild"  v-model="addFile" />

        <v-list>
            <!-- <v-subheader>Archivos</v-subheader> -->
            <v-btn  :loading="loading" :disabled="loading" color="blue-grey" class="ma-2 white--text" v-on:click ="añadirArchivo()"  >  
              Subir archivo  <v-icon right dark> mdi-cloud-upload </v-icon>
        </v-btn>
         <v-btn  :loading="loading" :disabled="loading" color="blue-grey" class="ma-2 white--text" v-on:click ="entrenar()"  >  
              Entrenar  <v-icon right dark> mdi-cloud-upload </v-icon>
        </v-btn>
            <v-list-item-group v-model="selectedItem" color="primary" style="max-height: 500px; " class="overflow-y-auto"
            >
            <v-list-item   v-for="(item, i) in filteredItems" :key="i">
                <v-list-item-icon>
                <v-icon v-text="'mdi-pencil'" ></v-icon>
                </v-list-item-icon>
                <v-list-item-content v-on:click = "openFile(item)" >
                    <v-list-item-title v-text="item.name"></v-list-item-title>
                </v-list-item-content>
            </v-list-item>

            </v-list-item-group>
        </v-list>
    <!-- </v-virtual-scroll> -->
      </v-col>



      <v-col >
          <!-- @click="loader = 'loading'" -->
        

        <v-sheet class="pa-12" color="grey lighten-3" elevation="24" style="max-height: 1000px; " height = "1000" >
        
        <v-btn v-if="textArea!=null" :loading="loading" :disabled="loading" color="blue-grey" class="ma-2 white--text" v-on:click ="uploadFile()"  >  
              Guardar cambios  <v-icon right dark> mdi-cloud-upload </v-icon>
        </v-btn>
        
        <v-container fluid v-if="textArea!=null" >
            <!-- label="Label" -->
            <v-textarea
            name="input-7-1"
            style="max-height: 1000px; " class="overflow-y-auto; text-left;"
            v-model="textArea"
            rows="30"
            row-height="30"
            :auto-grow="false"
            ></v-textarea>
        </v-container>

        </v-sheet>
        
      </v-col>


    </v-row>
  </v-container>


  </v-app>
</template>

<script lang="js">
import { Component, Vue } from 'vue-property-decorator';
import  UploadFileComponent  from "../components/UploadFileComponent.vue";

import axios from 'axios'


export default{
    data(){
        return{
            elevations: [6, 12, 18],
            selectedItem: null,
            items: [
            { name: 'Real-Time'},
            ],
            textArea:null,
            test:"hola",
            loading:false,
            file:null,
            addFile:false,
            search:"",
        }
    },
    computed: {
    filteredItems() {
        return this.$data.items.filter((item) =>{
            return item.name.toLowerCase().match(this.$data.search)  
        });
    }
  },
    methods: {
      
        getFiles() {
            // console.log(this.$data.test); // Our Vue component
            axios.get('http://127.0.0.1:3333/admin/files', {
                params: {
                }
            })
            .then(response => {
                const array = []
                for (let index = 0; index < response.data.length; index++) {
                    // console.log(response.data[index]);
                    array.push(response.data[index])   
                }   
                this.$data.items = array
                console.log(this.$data.items);
                // console.log("soy array "+array[0].name);
                return array;
            })
            .catch(function (error) {
                console.log(error);
            })            
        },
        openFile(file){
            console.log(file.name);

            axios.get('http://127.0.0.1:3333/admin/file', {
                params: {
                    path:file.path,
                    token:"token"
                }
            })
            .then(response => {
               
                
                console.log(response.data);
                this.$data.textArea = response.data
                if(response.data == undefined){
                  this.$data.textArea=""
                }
                this.$data.file = file
                // console.log("soy array "+array[0].name);
                // return array;
            })
            .catch(function (error) {
                console.log(error);
            })   
            
        },
        uploadFile(){
            console.log(this.$data.file.path);
            this.$data.loading = true;
            // const path = this.$data.file.path
            // const content = this.$data.file.textArea
            const post = {
                    path:this.$data.file.path,
                    token:"token",
                    content:this.$data.textArea
            };
            axios.post('http://127.0.0.1:3333/admin/file', post ).then(response => {
               
                this.$data.loading=false;
                console.log(response.data);

            })
            .catch(function (error) {
                console.log(error);
            })   
            
        },
        añadirArchivo(){
          this.$data.addFile=true;
        },
        entrenar(){
          axios.get('http://127.0.0.2:3333/chatbot/entrenar')
            .then(response => {
               
                
                console.log(response.data);
            })
            .catch(function (error) {
                console.log(error);
            })  
        },
        checkUpload(data){
          console.log("me cerre");
          console.log(data);
        },
        onClickChild (value) {
          console.log(value) // someValue
          if (value) {
            this.getFiles();
          }
        },
       
    },
    mounted(){
        // console.log(process.env.BASE_URL);
        // console.log("process.env.BASE_URL");
        this.getFiles();
        // console.log(this.$data.item);
        
    },
    components: {
      UploadFileComponent
    }
}

</script>
<style scoped>
  .custom-loader {
    animation: loader 1s infinite;
    display: flex;
  }
  @-moz-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-webkit-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-o-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>
