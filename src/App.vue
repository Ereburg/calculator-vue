<template>
  <div id="app">
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue';

export default {
  name: 'app',
  components: {
    Calculator,
  },
};
</script>

<style>
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: rgb(202, 201, 201);
}

#app {
  max-width: 100vw;
  width: 100%;
  height: calc(100vh - 16px);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Roboto', 'Avenir', Helvetica, Arial, sans-serif;
  font-weight: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

@media screen and (max-width: 500px) {
  #app {
    height: 100vh;
    background: #494949;
  }
}
</style>
