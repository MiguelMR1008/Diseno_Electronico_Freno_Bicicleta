<template>
 <!--div id= "homeScreen">
	<h1>MENU PRINCIPAL</h1><br>

    <h1>Bienvenido {{nombre}} {{apellido}}</h1><br>
	<button type="button" v-on:click="login()">Ubicación actual</button><br><br>
	<button type="button" v-on:click="goUbicaciones()">Registros ubicación</button><br><br>
	<button type="button" v-on:click="login()">Estado del dispositivo</button><br><br>
	<button type="button" v-on:click="goConfig()">Configuración</button><br><br>
	<button type="button" v-on:click="goRegDisp()">Registrar dispositivo</button><br><br>

 </div-->
 
 <div class="homeScreen">
 	<h1>Bienvenido {{nombre}} {{apellido}}</h1><br>
  <ul class="nav">
    <li class="nav-item">
      <button type="button" v-on:click="goUbicaciones()">Registros ubicación</button><br><br>
    </li>
    <li class="nav-item">
      <button type="button" v-on:click="goEstado()">Estado del dispositivo</button><br><br>
    </li>
    <li class="nav-item">
      <button type="button" v-on:click="goConfig()">Configuración</button><br><br>
    </li>
  </ul>
</div>

</template>

<script>
	import axios from 'axios';
	export default {
		name: 'Registros',
		data(){
			return{
				nombre: localStorage.nombreUsuario,
				apellido: localStorage.apellidoUsuario,
				registros: null,
				variable: null,
				IDdisp: null,
				intensidadGolpe: null,
				latitud: null,
				longitud: null,
				nivelBateria: null,
				fechaRegis: null,
			};
		},
		created: function(){
			const headers = {
                'acces-token' : localStorage.tokenSession,
                'Authorization' : 'JWT fefege...'
            }
            var data = {
            	correo : ""
            }
            axios.post('http://localhost:3000/consultaToken',data,{
                headers : headers
            })
            .then(res =>{
            	if(res.data.codigo == 0){
            		this.$router.push("/")
      				localStorage.estadoSesion = "Usuario no autenticado. Inicie sesión";
            	}
            })
		},
		methods:{
			goRegDisp(){
				this.$router.push("/config")
			},
			goUbicaciones(){
				this.$router.push("/data")
			},
			goEstado(){
				this.$router.push("/estadodis")
			},
			goConfig(){
				this.$router.push("/config")
			}
		},
	}
</script>

<style>
	h3 {
		margin-bottom: 5%;
	}
</style>