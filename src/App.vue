<script>
import CryptoDashboard from './components/CryptoDashboard.vue'
export default {
  name: 'app',
  components: {
    CryptoDashboard
  }
}
</script>

<template>
  <div id="app">
    <CryptoDashboard />
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(-45deg, #0f2027, #203a43, #2c5364, #1e3c72);
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
  color: #fff;
  min-height: 100vh;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
