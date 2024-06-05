<template>
  <div id="app">
    <h1 class="text-center py-3">AzarChat</h1>
    <h2 class="text-center">Recarga la pagina (press F5) y cambia tu chat</h2>
    <main class="my-5 container">
      <div class="row g-4">
        <div class="col-3">
          <CardUser :usuario="usuarios[0]" @enviarMensaje="enviarMensajeHandler" />
        </div>
        <div class="col-5 d-flex">
          <ChatUser :mensajes="mensajes" :usuarios="usuarios"/>
        </div>
        <div class="col-3">
          <CardUser :usuario="usuarios[1]" @enviarMensaje="enviarMensajeHandler" />
        </div>
      </div>
    </main>
  </div>
</template>


<script>
// importamos axios para llamar a las apis
import axios from 'axios';
import CardUser from './components/CardUser.vue';
import ChatUser from './components/ChatUser.vue';

export default {
  name: 'App',
  components: {
    CardUser,
    ChatUser,
  },
  data() {
    return {
      usuarios: [],
      mensajes: [],
    }
  },
  // este método es el que llama a la información de la api, por eso usamos axios.get y lo controlamos con el try
  methods: {
    async getPerson() {
      try {
        let response = await axios.get("https://randomuser.me/api/?results=2")
        this.usuarios = response.data.results
        // console.log(response)

      } catch (error) {
        console.log(error)
      }
    },
    // Contruimos la funcion que crea el objeto "nuevo mensaje" y que se agrega (push) al array Mensajes en data
    enviarMensajeHandler(mensaje) {
            let nuevoMensaje = {
                id: mensaje.id,
                color: mensaje.color,
                nombreCompleto: mensaje.nombreCompleto,
                texto: mensaje.texto
            }
            this.mensajes.push(nuevoMensaje)
        }
  },
  // Metodo de Ciclo de vida - aca decimos que apenas se monte el Dom Ejecute la función "getPerson"
  mounted() {
    this.getPerson()
  }
}
</script>

<style>


main {
  background-image: url(../src/assets/fondoChat.jpg);
  ;
}
</style>
