
<template>
  <nav class="navbar">
    <div class="nav-brand">
      <router-link to="/">  
        <div> </div>
        <div class="logo">
            <img src="/logo_hpm.svg" alt="Logo" class="logo-image" />
            <span>Hecho en</span>
            <strong>Puerto Morelos</strong>
        </div>
      </router-link>
    </div>

    <!-- Botón Hamburguesa para Móvil -->
    <button class="menu-toggle" @click="toggleMenu" :aria-expanded="isMenuOpen">
      <span class="bar"></span>
      <span class="bar"></span>
      <span class="bar"></span>
    </button>

    <!-- Enlaces de Navegación -->
    <ul class="nav-links" :class="{ 'is-open': isMenuOpen }">
      <li v-for="(link, index) in links" :key="index">
        <router-link 
        :to="link.path" 
        @click="closeMenu"
        :class="{ 'nav-btn': link.isButton }">
          {{ link.label }}
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { ref } from 'vue'

// Definición de Props
defineProps({
  links: {
    type: Array,
    required: true
  }
})

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<style scoped>

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #ffffff;
  color: #000000;
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-brand a {
  
  
  text-decoration: none;
}

.logo {
  display: flex;
  flex-direction: column;
  line-height: 1.1;
}

.logo span {
  color: #465452;
  font-size: 0.72rem;
  font-weight: 600;
}

.logo strong {
  color: #0d9488;
  font-size: 1rem;
}

.logo-image {
  height: 40px; 
  width: auto;
  
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 1.5rem;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: #171414;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s ease;
}


.nav-links a:hover {
  color: #fcd34d;
}

.nav-links a.router-link-active {
  color: #42b983; 
  font-weight: bold;

}

.nav-links a.nav-btn {
  background-color: #0d9488; 
  color: hsl(0, 0%, 100%);          
  padding: 0.8rem 1.25rem;   
  border-radius: 0.6rem;        
  font-weight: bold;
  transition: background-color 0.2s ease, transform 0.1s ease;
}


.nav-links a.nav-btn:hover {
  background-color: #0f766e; 
  color: #ffffff;
}


.nav-links a.nav-btn.router-link-active {
  background-color: #0f766e; 
  color: #8be1ba;
  box-shadow: 0 0 10px rgba(66, 185, 131, 0.5);
}

/* Botón Hamburguesa */
.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}

.menu-toggle .bar {
  width: 25px;
  height: 3px;
  background-color: #0f766e;
  border-radius: 2px;
}

/* Diseño Responsivo (Móvil) */
@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
  }

  .nav-links {
    display: none; 
    flex-direction: column;
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: #ffffff;
    padding: 1rem 0;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .nav-links.is-open {
    display: flex; 
  }

  .nav-links li {
    text-align: center;
    padding: 0.75rem 0;
  }
}
</style>
