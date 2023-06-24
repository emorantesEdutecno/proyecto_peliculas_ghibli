<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!--
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  -->
  <Bienvenida
    v-on:iniciar="consumirAPI"
    v-on:permitirPeliculas="mostrarComponentePeliculas"
    v-bind:terminado="mensaje"
  />

  <div v-if="mostrarPeliculas">
        <Peliculas 
        v-bind:datosPeliculas="datosConsumidos"
      />
  </div>


</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Bienvenida from '@/components/Bienvenida.vue';
import Peliculas from '@/components/Peliculas.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Bienvenida,
    Peliculas
  },
  data:function(){
    return{
        mensaje:'',
        datosConsumidos:[],
        mostrarPeliculas: false,
    }
  },
  methods:{
    consumirAPI: function(flag){
      this.mensaje='...Consumiendo API, por favor espere';
      if(flag==true){
        let url='https://ghibliapi.vercel.app/films';
        fetch(url)
        .then(respuesta=> respuesta.json())
              .then(datosJson =>{

                let timeout= 3000;
                setTimeout(() => {
                  this.mensaje = 'Se terminó de consumir la API después de 10 segundos';
                  this.datosConsumidos = datosJson;
                  console.log(datosJson);
                }, timeout);
                

              })
        .catch(error=> console.log('Error consumiendo API', error));
      }else{
        console.log('Error desconocido');
      }

    },
    mostrarComponentePeliculas:function(autorizacion){
      if(autorizacion== true){
        this.mostrarPeliculas = true;
      }
    },

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
