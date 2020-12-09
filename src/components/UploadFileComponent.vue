<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
    
      max-width="290"
    >
      
      <v-card>
        <v-card-title class="headline">
          Seleccione un archivo 
        </v-card-title>
        
        <v-card-text>
            <v-file-input
                chips
                v-model="files"
                accept=".aiml.kb, .txt "
                label="Archivo"
            ></v-file-input>    
        </v-card-text>
        
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="error"
            text
            @click="dialog = false"
            v-on:click="notUpload()"

          >
            Cancelar
          </v-btn>
          <v-btn
            color="green darken-1"
            text
            v-on:click="upload(dialog)"
          >
            Subir {{dialog}}
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import axios from 'axios'
  export default {
      props:{
          value:Boolean
      },
    computed: {
        dialog: {
            get () {
                return this.value
            },
            set (value) {
                this.$emit('input', value)
                this.$emit('close')
            }
        }
    },
    methods:{
        upload(dialog){
            // console.log(this.files.name);
            if(this.files.length!=0){
                console.log(this.files);
                const reader = new FileReader()
                let texto = "";
                texto ="1"
                //  reader.onload = e => (texto = e.target.result + texto)    
                
                reader.readAsText(this.files);
                reader.onload = () => {
                  // this.$data.content = reader.result;

                  const post = {
                    content:reader.result,
                    token:"token",
                    name:this.files.name 
                    
                  };
                  axios.post('http://127.0.0.1:3333/admin/addFile ', post ).then(response => {
                      
                      this.$emit('input', false)
                      this.$emit('clicked', true)

                  })
                  .catch(function (error) {
                      this.$emit('input', false)
                      this.$emit('clicked', false)
                      console.log(error);
                  })

                }
                 
                // console.log(reader.readAsText(this.files));              

                 
            
            }
        },
        notUpload(){
            this.$emit('clicked', false)
        }

    },
    data () {
      return {
        files: [],
        content:""
      }
    },
  }
</script>