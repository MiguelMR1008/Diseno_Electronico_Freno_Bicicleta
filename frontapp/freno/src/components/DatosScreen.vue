<template>
 <div class= "data"><br><br>
	<div>{{variable}}</div>
	<table class="table">
		<thead>
			<th scope="col">IDDispositivo</th>
			<th scope="col">Latitud</th>
			<th scope="col">Longitud</th>
			<th scope="col">Nivel batería</th>
			<th scope="col">Fecha</th>
		</thead>
		<tbody>
			<tr v-for="dato in datos">
				<td>{{dato.IDdisp}}</td>
				<td>{{dato.latitud}}</td>
				<td>{{dato.longitud}}</td>
				<td>{{dato.nivelBateria}}</td>
				<td>{{dato.fechaRegis}}</td>
			</tr>
		</tbody>
	</table>
 </div>

</template>

<script>
	import axios from 'axios';
	export default {
		name: 'Datos',
		data(){
			return{
				dispositivos: null,
				datos: [],
				variable: null,
				correo: null,
				clave: null,
				data: null,
				headers: null,
				cont: 0,
			};
		},
		created: function(){
			this.headers = {
                'acces-token' : localStorage.tokenSession,
                'Authorization' : 'JWT fefege...'
            }
            this.data = {
            	request: " "
            }
            axios.post('http://localhost:3000/consultaDispositivos',this.data,{
                headers : this.headers
            }).then(res =>{
            	if(res.data.codigo != 0){

            		this.dispositivos = res.data



            		//this.variable = this.dispositivos.length
            		var i
            		for( i=0; i < 3; i++){
            			this.cont=this.cont+1;
            			this.data={
            				IDdisp : this.dispositivos[i]._id
            			}
            			axios.post('http://localhost:3000/consultaDatos',this.data,{
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
			verDato: function (lati, long){
				this.variable= " Latitud: " + lati.toString() + " Longitud: " + long.toString()
			}
		}
	}
</script>

<style>
	h3 {
		margin-bottom: 5%;
	}
</style>