<template>
 <div><br><br>

 	<!--Mapa 
	 :recibirCoordenadas="recibirCoordenadas"
	  @verregistro="Prueba($event)"
	/-->	
	<h2>{{variable}}</h2>			
	<table class="table">
		<thead>
			<th scope="col">ID</th>
			<th scope="col">IDDispositivo</th>
			<th scope="col">Bateria</th>
			<th scope="col">Fecha</th>
		</thead>
		<!--buttonbutton v-on:click="verDato(23)" ></button-->
		<tbody>
			<tr v-for="dato in datos">
				<td>{{dato._id}}</td>
				<td>{{dato.IDdisp}}</td>
				<td>{{dato.nivelBateria}}</td>
				<td>{{dato.fechaRegis}}</td>
			</tr>
		</tbody>
	</table>
			
			<!--button @click="$emit('verregistro','hola')">Pasar dato</button-->
 </div>

</template>

<script>

	//Variable bus datos

	import axios from 'axios';
	export default {
		name: 'EstadoDisp',
	 	data(){
			return{
				dispositivos: null,
				nombresdisp: [],
				datos: [],
				variable: null,
				variable2: null,
				variable3: null,
				correo: null,
				correoAsociado: null,
				nombreUsuario: null,
				data: null,
				headers: null,
				cont: 0,
				visible: null,
				//Variables mapa
			};
		},
		created: function(){
			this.headers = {
                'acces-token' : localStorage.tokenSession,
                'Authorization' : 'JWT fefege...'
            }
	        		this.data = {
				        req : " "
				    }
	        		axios.post('http://localhost:3000/consultaDispositivos',this.data,{
		                headers : this.headers
		            }).then(res =>{
		            	if(res.data.codigo != 0){
		            		this.dispositivos = res.data
		            		var i
		            		for( i=0; i < this.dispositivos.length; i++){
		            			this.cont=this.cont+1;
		            			this.data={
		            				IDdisp : this.dispositivos[i]._id
		            			}
		            			axios.post('http://localhost:3000/ultimoDato',this.data,{
					                headers : this.headers
					            }).then(res =>{
					            	if(res.data.codigo != 0)
					            		//this.datos.push(res.data)
					            		this.datos = this.datos.concat(res.data)
					            	
								})
		            		}
		            	}else{
		            		this.$router.push("/")
		      				localStorage.estadoSesion = "Usuario no autenticado. Inicie sesión";
		            	}
					})
		},		
		methods:{
			Prueba(dato){
				alert(dato);
				}
		}
	}
</script>

<style>
	h3 {
		margin-bottom: 5%;
	}
</style>