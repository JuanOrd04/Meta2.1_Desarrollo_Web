<script setup>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import IndexPage from './pages/index.vue'
</script>

<template>
  <v-app>
    <!-- Encabezado de la aplicación -->
    <AppHeader />
    
    <!-- Contenido principal -->
    <v-main>
      <IndexPage />
    </v-main>

    <!-- Pie de página -->
    <AppFooter />
  </v-app>
</template>

<style>
/* Estilos globales básicos */
body {
  margin: 0;
  font-family: sans-serif;
}
</style>
