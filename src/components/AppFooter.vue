<script setup>
import { computed } from 'vue'

const currentDate = computed(() => {
  const date = new Date()
  return date.toLocaleDateString('es-ES', { 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric' 
  })
})

const currentYear = computed(() => new Date().getFullYear())
</script>

<template>
  <v-footer color="grey-lighten-4" class="pa-4 text-center d-flex flex-column border-top">
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="4" class="py-2">
          <strong>Nombre:</strong> Juan Pérez <!-- Cambiar por el nombre real -->
        </v-col>
        <v-col cols="12" sm="4" class="py-2">
          <strong>Matrícula:</strong> 01234567 <!-- Cambiar por la matrícula real -->
        </v-col>
        <v-col cols="12" sm="4" class="py-2">
          <strong>Fecha:</strong> {{ currentDate }}
        </v-col>
      </v-row>
      <v-divider class="my-4"></v-divider>
      <v-row>
        <v-col cols="12">
          &copy; {{ currentYear }} - Portafolio Universitario. Todos los derechos reservados.
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<style scoped>
.border-top {
  border-top: 1px solid #e0e0e0;
}
</style>
