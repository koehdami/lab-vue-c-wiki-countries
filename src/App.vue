<template>
  <div class="app">
    <Navbar></Navbar>
    <RouterView></RouterView>
  </div>
</template>

<script>
  import Navbar from "./components/Navbar.vue"
  export default {
    components:{
      Navbar
    }
  }
</script>

<style></style>