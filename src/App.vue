<template>
  <div id="app">
    <Fruits/>
  </div>
</template>

<script>
import Fruits from './components/Fruits';

export default {
  name: 'App',
  components: {
    Fruits,
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
