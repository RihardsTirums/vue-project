<script setup lang="ts">
import { RouterView, RouterLink } from 'vue-router';
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';
</script>

<template> 
<nav class="m-3">
  <RouterLink class="text-design" to="/">Home</RouterLink>
  <RouterLink class="text-design2" to="/about">About</RouterLink>
  <RouterLink class="text-design3" to="/characters">Characters</RouterLink>
  <RouterLink class="text-design3" to="/form">Form</RouterLink>
</nav>
  <RouterView/>
</template>

<style scoped>
  nav{
    display: flex;
    column-gap: 10px;
  }
    .text-design{
      color: rgb(253, 173, 0);
      text-decoration: none;
      font-size: 20px;
    }
    .text-design2{
      color: rgb(1, 67, 129);
      text-decoration: none;
      font-size: 20px;
    }
    .text-design3{
      color: rgb(112, 8, 8);
      text-decoration: none;
      font-size: 20px;
    }
  
</style>
