<template class="fondo-style">
  <div id="app">
    <Presentacion :showCard="showCard" @toggleCard="toggleCard" />
    <Api v-if="showCard" />
  </div>
</template>

<script>
import Presentacion from './components/Presentacion.vue'
import Api from './components/Api.vue'

export default {
  name: 'App',
  components: {
    Api,
    Presentacion
  },
  data() {
    return {
      showCard: false,
    };
  },
  methods: {
    toggleCard() {
      this.showCard = !this.showCard;
    },
  },
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
