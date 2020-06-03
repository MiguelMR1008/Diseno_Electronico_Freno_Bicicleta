<template>
  <div class="inicio">
    <img style="width:500px;height:300px" alt="Logo" src="../assets/imagenFreno.png">
    <Login />
  </div>
</template>

<script>
// @ is an alias to /src
import Login from '@/components/Login.vue'

export default {
  name: 'Inicio',
  /*data(){
  	return{
  		variable: localStorage.estadoSesion,
  	};
  },*/
  components: {
    Login
  }
}
</script>
