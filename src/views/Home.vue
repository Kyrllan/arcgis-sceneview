<template>
  <div>
    <section class="bg-red-500">
      <h1>Sessão 1</h1>
    </section>
    <section class="bg-green-500">
      <div id="mapContainer"></div>
    </section>
    <section class="bg-blue-500">
      <h1>Sessão 3</h1>
      <button class="bg-primary py-1 px-2 rounded-lg hover:opacity-90 text-white">Botão</button>
    </section>
  </div>
</template>

<script setup>
import Map from '@arcgis/core/Map'
import SceneView from '@arcgis/core/views/SceneView.js'
import SceneLayer from '@arcgis/core/layers/SceneLayer.js'
import { onMounted } from 'vue'

let view = null
let map = null

onMounted(() => {
  const sceneLayer = new SceneLayer({
    url: 'https://services.arcgis.com/V6ZHFr6zdgNZuVG0/arcgis/rest/services/Paris_3D_Local_WSL2/SceneServer/layers/0'
  })

  map = new Map({
    basemap: 'topo-3d',
    ground: 'world-elevation',
    layers: [sceneLayer]
  })

  view = new SceneView({
    map,
    container: 'mapContainer',
    camera: {
      position: {
        // Define a posição da câmera
        x: -51.2277, // Longitude de Porto Alegre
        y: -30.045, // Latitude de Porto Alegre
        z: 1000 // Altura em metros acima do nível do mar
      },
      tilt: 60, // Inclinação da câmera
      heading: 0 // Direção para onde a câmera está apontada (em graus)
    }
  })
})
</script>

<style lang="scss" scoped>
section {
  height: 100vh;
}

#mapContainer {
  width: 100%;
  height: 100%;
}
</style>
