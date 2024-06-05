<template>
  <div id="card__person" class="container">
    <div class="card" style="width: 18rem;">
      <img :src="usuario.picture.large" class="card-img-top" alt="...">
      <div class="card-body">
        <h5 class="card-title text-center">{{ nombreCompleto }}</h5>
        <form action="">
          <p class="card-body-color">Selecciona el fondo de tu texto</p>
          <input class="form-control mb-2" type="color" name="color" id="color" v-model="mensaje.color">
          <textarea class="form-control" name="chat" id="chat" v-model="mensaje.texto"
            @keyup.enter="enviarMensaje"></textarea>
          <button @click.prevent="enviarMensaje" class="btn btn-primary my-2">Enviar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardUser',
  // Los props son el Metodo para recibir informacion desde el padre, en este caso recibe el objeto creado en la data de app.vue
  props: {
    usuario: Object,
  },
  //creamos en data las variables a ocupar 
  data() {
    return {
      mensaje: {
        texto: "",
        color: "",
        id: "",
      },

    }
  },
  // dado que en la API el obtener lo valores debemos ingresa a muchos datos, usamos la propiedad computed para simpificar la informaicion
  computed: {
    nombreCompleto() {
      return `${this.usuario.name.first} ${this.usuario.name.last}`;
    }
  },
  // creamos el metodo enviar mensaje para "emitir" (enviar) la informaciond el hijo al padre (App.vue)
  methods: {
    enviarMensaje() {
      this.mensaje.id = this.usuario.id.value;
      this.mensaje.nombreCompleto = this.nombreCompleto;
      this.$emit("enviarMensaje", this.mensaje)
      this.mensaje.texto = "";
    }
  },
  created() {
    console.log(this.usuario)
  }

}
</script>

<style scoped>
.card-body {
  background-color: white;
}

.card-body-color{
  font-size: 12px;
  text-align: center;
}
</style>
