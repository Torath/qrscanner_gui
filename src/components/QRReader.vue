<template>
  <div id="QRReader" v-if="response_sn === null">
      <h3> Wybierz plik ze zdjęciem panelu aby odczytać numer seryjny (SN)</h3>
      <input type="file" id="file" ref="file" accept="image/jpeg" @change=uploadImage()>
      <br><button v-on:click="submitFile()">Wyślij</button>
      <div v-if="err">{{ err }}</div>
  </div>
  <div v-else>
      Odczytany numer seryjny panelu to:
      {{response_sn}}
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'QRReader',
  data(){
        return{
            err:null,
            image:null,
            response_sn: null
        }
  },
  methods: {
      uploadImage() {
          this.err = null
          this.image = this.$refs.file.files[0];
      },
      submitFile(){
          let formData = new FormData();
          formData.append('img', this.image)
          axios.post('http://torath.pythonanywhere.com',
            formData,
            {
                headers: {
                    'Content-Type': 'multipart/form-data'
                }
            }
          ).then(response => {
              this.response_sn = response.data.data.SN
              console.log(response)
          }).catch(error => {
              this.err = error
              this.err += "\n Niepoprawny plik. Sprawdź czy na pewno jest na nim widoczny kod QR" 
          })
      }
  }
}
</script>