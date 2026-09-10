<script setup>
// Datos fijos del perfil del estudiante (4 filas, 3 columnas)
const habilidades = [
  { tecnica: 'HTML, CSS y JavaScript', nivel: 'Intermedio', experiencia: '2 años' },
  { tecnica: 'Vue 3 & Vuetify', nivel: 'Básico', experiencia: 'Menos de 1 año' },
  { tecnica: 'Git y GitHub', nivel: 'Intermedio', experiencia: '2 años' },
  { tecnica: 'Consumo de APIs REST', nivel: 'Básico', experiencia: '1 año' }
]
</script>

<template>
  <v-card class="elevation-3">
    <v-card-title class="text-h6 text-center pa-4 bg-grey-lighten-4">
      Habilidades Técnicas
    </v-card-title>
    
    <v-table hover>
      <thead>
        <tr>
          <th class="text-left text-subtitle-1 font-weight-bold">Habilidad Técnica</th>
          <th class="text-left text-subtitle-1 font-weight-bold">Nivel de Dominio</th>
          <th class="text-left text-subtitle-1 font-weight-bold">Años de Experiencia</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in habilidades" :key="index">
          <td>{{ item.tecnica }}</td>
          <td>
            <v-chip size="small" :color="item.nivel === 'Intermedio' ? 'primary' : 'secondary'">
              {{ item.nivel }}
            </v-chip>
          </td>
          <td>{{ item.experiencia }}</td>
        </tr>
      </tbody>
    </v-table>
  </v-card>
</template>
