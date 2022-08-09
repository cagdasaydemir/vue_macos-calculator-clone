<template>
  <CalculatorComp></CalculatorComp>

</template>

<script>

import CalculatorComp from './components/CalculatorComp.vue'


export default {
  name: 'App',
  components: {

    CalculatorComp
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Work+Sans:wght@200&display=swap');

#app {
  font-family: 'Work Sans', sans-serif;
  text-rendering: optimizeLegibility;
  font-weight: 200;
  font-size: 30px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  box-sizing: border-box;

}

body {
  background: linear-gradient(90deg,
      #3b3c5c,
      #5d486e,
      #82537a,
      #a65e7f,
      #c86d7e,
      #e38078,
      #f69870,
      #ffb56b);
  background-size: cover;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
