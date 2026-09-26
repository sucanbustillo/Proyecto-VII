<template>
  <div id="app">

<NavBar :links="appNavigation" />
 <main class="content">
      <router-view />
    </main>
  </div>
</template>

<script setup>

import { ref } from 'vue'
import NavBar from './components/NavBar.vue'


const appNavigation = ref([
  { label: 'Inicio', path: '/' },
  { label: 'Explorar', path: '/Explorar' },
  { label: 'Categorías', path: '/Categorías' },
  { label: 'Soy Emprendedor', path: '/registro', isButton: true }
])
  
</script>

<style>
  /* Estilos generales */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
  }


</style>

