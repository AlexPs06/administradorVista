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
                accept=".txt"
                label="Archivo"
            ></v-file-input>    
        </v-card-text>
        
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="green darken-1"
            text
            @click="dialog = false"
            v-on:click="notUpload()"

          >
            Cancelar
          </v-btn>
          <v-btn
            color="green darken-1"
            text
            @click="dialog = true"
            v-on:click="upload()"
          >
            Subir
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
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
        upload(){
            this.$emit('clicked', true)
            // console.log(this.files.name);
            if(this.files!=null){
                console.log(this.files);
                const reader = new FileReader()

                reader.onload = e => console.log(e.target.result)    

                reader.readAsText(this.files)    
            }
        },
        notUpload(){
            this.$emit('clicked', false)
        }

    },
    data () {
      return {
        files: [],
      }
    },
  }
</script>