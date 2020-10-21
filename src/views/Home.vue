<template>
  <div class="home">
    <img id="logo" alt="Prodaso logo" src="../assets/logo.svg">
    <Dashboard />
  </div>
</template>

<script>
// @ is an alias to /src
import Dashboard from '@/components/Dashboard.vue'

export default {
  name: 'Home',
  components: {
    Dashboard
  }
}
</script>

<style scoped>
  #logo {
    width: 80px;
  }
</style>
