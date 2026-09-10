<script setup>
import { ref, onMounted } from 'vue'
import TarjetaConImagen from '../components/TarjetaConImagen.vue'
import TablaDeDatos from '../components/TablaDeDatos.vue'

// Estado para las dos tarjetas de imagen
const imagen1 = ref({ url: '', titulo: '', descripcion: '', autor: '' })
const imagen2 = ref({ url: '', titulo: '', descripcion: '', autor: '' })

// Estados de la interfaz (loading y manejo de errores)
const cargando = ref(false)
const errorApi = ref('')

// Función principal para consultar la API
const obtenerNuevasImagenes = async () => {
  // Preparamos los estados de carga
  cargando.value = true
  errorApi.value = ''

  try {
    // 1. Petición a la API usando fetch
    const respuesta = await fetch('https://picsum.photos/v2/list?page=1&limit=50')
    
    // Si la respuesta no es 200 OK, lanzamos error
    if (!respuesta.ok) {
      throw new Error('Hubo un problema de red al contactar la API')
    }

    // Convertimos la respuesta a JSON
    const datos = await respuesta.json()

    // 2. Seleccionamos dos imágenes aleatorias garantizando que sean distintas
    let indice1 = Math.floor(Math.random() * datos.length)
    let indice2 = Math.floor(Math.random() * datos.length)

    while (indice1 === indice2) {
      indice2 = Math.floor(Math.random() * datos.length)
    }

    const foto1 = datos[indice1]
    const foto2 = datos[indice2]

    // 3. Actualizamos nuestros datos usando las URLs como piden las instrucciones
    imagen1.value = {
      url: `https://picsum.photos/id/${foto1.id}/300/200`,
      titulo: 'Fotografía Aleatoria 1',
      descripcion: 'Esta es una imagen generada dinámicamente desde la API de Picsum.',
      autor: foto1.author
    }

    imagen2.value = {
      url: `https://picsum.photos/id/${foto2.id}/300/200`,
      titulo: 'Fotografía Aleatoria 2',
      descripcion: 'Esta es una imagen generada dinámicamente desde la API de Picsum.',
      autor: foto2.author
    }

  } catch (error) {
    // En caso de error, lo atrapamos y mostramos la alerta
    console.error(error)
    errorApi.value = 'No se pudieron cargar las imágenes. Revisa tu conexión de red o intenta de nuevo.'
  } finally {
    // Quitamos el estado de carga sin importar si funcionó o falló
    cargando.value = false
  }
}

// Opcional pero recomendado: Cargar un par de fotos apenas el usuario entre a la página
onMounted(() => {
  obtenerNuevasImagenes()
})
</script>

<template>
  <v-container class="py-8">
    
    <!-- Alerta de Error (Sólo se muestra si errorApi tiene texto) -->
    <v-row v-if="errorApi">
      <v-col cols="12">
        <v-alert type="error" variant="tonal" closable @click:close="errorApi = ''">
          {{ errorApi }}
        </v-alert>
      </v-col>
    </v-row>

    <!-- Área Principal: Tarjetas (Lado a lado en desktop, una debajo de otra en móvil) -->
    <v-row>
      <v-col cols="12" md="6" class="mb-4">
        <!-- Mostramos la tarjeta solo cuando ya tenemos URL -->
        <TarjetaConImagen 
          v-if="imagen1.url"
          :urlImagen="imagen1.url"
          :titulo="imagen1.titulo"
          :descripcion="imagen1.descripcion"
          :autor="imagen1.autor"
        />
        <!-- Esqueleto de carga opcional mientras llega el primer request -->
        <v-skeleton-loader v-else type="card"></v-skeleton-loader>
      </v-col>
      
      <v-col cols="12" md="6" class="mb-4">
        <TarjetaConImagen 
          v-if="imagen2.url"
          :urlImagen="imagen2.url"
          :titulo="imagen2.titulo"
          :descripcion="imagen2.descripcion"
          :autor="imagen2.autor"
        />
        <v-skeleton-loader v-else type="card"></v-skeleton-loader>
      </v-col>
    </v-row>

    <!-- Botón de actualización: Centrado entre tarjetas y tabla -->
    <v-row class="my-6">
      <v-col class="text-center">
        <v-btn
          color="primary"
          size="x-large"
          prepend-icon="mdi-refresh"
          :loading="cargando"
          :disabled="cargando"
          @click="obtenerNuevasImagenes"
        >
          Actualizar Imágenes
        </v-btn>
      </v-col>
    </v-row>

    <!-- Tabla de datos ocupando el ancho completo -->
    <v-row>
      <v-col cols="12">
        <TablaDeDatos />
      </v-col>
    </v-row>
  </v-container>
</template>
