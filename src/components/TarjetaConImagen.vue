<script setup>
defineProps({
  urlImagen: {
    type: String,
    required: true
  },
  titulo: {
    type: String,
    required: true
  },
  descripcion: {
    type: String,
    required: true
  },
  autor: {
    type: String,
    required: true
  }
})
</script>

<template>
  <v-card class="mx-auto elevation-3" max-width="500">
    <!-- Imagen de la tarjeta -->
    <v-img :src="urlImagen" height="250px" cover></v-img>
    
    <!-- Título de la tarjeta -->
    <v-card-title>{{ titulo }}</v-card-title>
    
    <!-- Subtítulo con el autor -->
    <v-card-subtitle>Fotografía por: {{ autor }}</v-card-subtitle>
    
    <!-- Descripción -->
    <v-card-text>
      {{ descripcion }}
    </v-card-text>
  </v-card>
</template>
