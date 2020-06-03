<template>
  <div class="config">
    <div id="nave">
      <div>
      <router-link to="/home">Volver</router-link></div>
    </div>
    <h1>Configuración</h1>
      <ul class="nav">
    <li class="nav-item">
      <RegistroDispositivo />
    </li>
    <li class="nav-item">
      <Config />
    </li>
  </ul>
    <!--Config />
    <RegistroDispositivo /-->
  </div>

  <!--div id="nave" class="config">
      <section>
          <b-tabs position="is-centered" class="block">
              <b-tab-item label="Pictures"></b-tab-item>
              <b-tab-item label="Music"></b-tab-item>
              <b-tab-item label="Videos"></b-tab-item>
          </b-tabs>
          <b-tabs position="is-right" class="block">
              <b-tab-item label="Pictures"></b-tab-item>
              <b-tab-item label="Music"></b-tab-item>
              <b-tab-item label="Videos"></b-tab-item>
          </b-tabs>
      </section>
  </div-->
</template>

<script>
// @ is an alias to /src
import RegistroDispositivo from '@/components/RegistroDispositivo.vue'
import Config from '@/components/Config.vue'

export default {
  name: 'Configuracion',
  components: {
    RegistroDispositivo,
    Config
  }
}
</script>

<style>
    #nave {
      padding: 30px;
    }

    #nave a {
      font-weight: bold;
      color: #2c3e50;
    }

    #nave a.router-link-exact-active {
      color: #42b983;
    }
</style>