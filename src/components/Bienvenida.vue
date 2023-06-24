<template>
    <div id="Bienvenida">
        <h1>Componente Bienvenida</h1>
        <h3>{{  mensajeEspera }}</h3>

        <hr>

        <div id="divIngresar" v-if="mostrarDivIngresar">
            <button v-on:click="procesarBienvenida">Ingresar</button>
        </div>



        <div id="formularioDatos" v-if="!mostrarDivIngresar">
            <form>
                <label for="txtNombre">Nombre:</label>
                <input type="text" id="txtNombre" v-model="nombre"><br>
                <label for="txtApellido">Apellido:</label>
                <input type="text" id="txtApellido" v-model="apellido"><br>
                <!--
                  <button id="btnEnviar" v-on:click.prevent="presentarBienvenida">Enviar</button>
                -->
                <input type="submit" id="btnEnviar" v-on:click.prevent="presentarBienvenida" value="Enviar">
                

            </form>

        </div>

        <div id="mensajeBienvenida" v-if="mostrarMensajeBienvenida">
            <p>Bienvenid@ {{  nombre }} {{  apellido }} </p>
            <p>Aquí podrás encontrar información de películas de anime de Studios Ghibli</p>
            <button v-on:click="limpiarInfo"> Limpiar información</button>
        </div>


    </div>
</template>

<script>
export default{
    name:'Bienvenida',
    props:{
        terminado:{
            type: String,
            required:true,
        },

    }, 
    data:function(){
        return{
            mostrarDivIngresar: true,
            mostrarMensajeBienvenida: false,
            nombre: '',
            apellido:'',
        }
    },
    methods:{
        procesarBienvenida:function(){
            this.$emit('iniciar', true);
            this.mostrarDivIngresar = false;
        },
        presentarBienvenida: function(){
            // console.log('presentar bienvenida');
            this.mostrarMensajeBienvenida = true;
            this.mostrarDivIngresar = true;
            this.$emit('permitirPeliculas', true);
        },
        limpiarInfo:function(){
            this.mostrarMensajeBienvenida = false;
        },
    },
    computed:{
        mensajeEspera:function(){
            return this.terminado;
        },
    }
}
</script>

<style scoped>
#Bienvenida{
    background-color: coral;
}
</style>