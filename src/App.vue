<script setup lang="ts">
import { RouterView, RouterLink } from 'vue-router'
</script>

<template> 
<nav>
  <RouterLink to="/">Home</RouterLink>
  <RouterLink to="/about">About</RouterLink>
  <RouterLink to="/characters">Characters</RouterLink>
</nav>
  <RouterView/>
</template>

<style scoped>
  nav{
    display: flex;
    column-gap: 10px;
  }
    
  
</style>
