<template>
  <div id="app">
    <Actividad/>
  </div>
</template>

<script>
import Actividad from './components/Actividad';

export default {
  name: 'App',
  components: {
    Actividad,
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
