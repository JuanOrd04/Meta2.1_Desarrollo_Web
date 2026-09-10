<script setup>
import TarjetaConImagen from '../components/TarjetaConImagen.vue'
import TablaDeDatos from '../components/TablaDeDatos.vue'

// Datos iniciales estáticos para cumplir con la Parte 2. 
// En la Parte 3, estos datos serán reemplazados por los de la API.
const imagen1 = {
  url: 'https://picsum.photos/id/10/300/200',
  titulo: 'Bosque en la Niebla',
  descripcion: 'Una fotografía que muestra un paisaje boscoso muy tranquilo.',
  autor: 'Paul Jarvis'
}

const imagen2 = {
  url: 'https://picsum.photos/id/11/300/200',
  titulo: 'Camino Natural',
  descripcion: 'Un sendero hermoso para caminar rodeado de naturaleza salvaje.',
  autor: 'Paul Jarvis'
}
</script>

<template>
  <v-container class="py-8">
    <!-- Fila para las dos tarjetas. En escritorio mitad y mitad, en móvil ancho completo -->
    <v-row>
      <v-col cols="12" md="6" class="mb-4">
        <TarjetaConImagen 
          :urlImagen="imagen1.url"
          :titulo="imagen1.titulo"
          :descripcion="imagen1.descripcion"
          :autor="imagen1.autor"
        />
      </v-col>
      <v-col cols="12" md="6" class="mb-4">
        <TarjetaConImagen 
          :urlImagen="imagen2.url"
          :titulo="imagen2.titulo"
          :descripcion="imagen2.descripcion"
          :autor="imagen2.autor"
        />
      </v-col>
    </v-row>

    <!-- Espacio para el botón de la Parte 3 centrado -->
    <v-row class="my-4">
      <v-col class="text-center">
        <!-- El botón se agregará en la Parte 3 -->
        <p class="text-grey mb-0">(El botón de actualización de la API se agregará aquí en la Parte 3)</p>
      </v-col>
    </v-row>

    <!-- Tabla de datos ocupando todo el ancho -->
    <v-row>
      <v-col cols="12">
        <TablaDeDatos />
      </v-col>
    </v-row>
  </v-container>
</template>
