<script lang="ts">
  import MapView from '@arcgis/core/views/MapView'
  import '@arcgis/core/assets/esri/themes/light/main.css'
  import GraphicsLayer from '@arcgis/core/layers/GraphicsLayer'
  import Graphic from '@arcgis/core/Graphic'
  import SimpleMarkerSymbol from '@arcgis/core/symbols/SimpleMarkerSymbol'
  import Point from '@arcgis/core/geometry/Point'

  const createMap = (domNode: any) => {
    const view = new MapView({
      container: domNode,
      map: {
        basemap: 'streets-vector',
      },
      zoom: 15,
      center: [172.6362, -43.5321], // longitude, latitude
    })
    // Create a graphics layer for points of interest
    const graphicsLayer = new GraphicsLayer()
    view.map.add(graphicsLayer)
    // Create a simple marker symbol
    const markerSymbol = new SimpleMarkerSymbol({
      color: [226, 119, 40], // RGB color for the marker
      size: 10, // Size of the marker
      outline: {
        color: [255, 255, 255], // Outline color
        width: 1, // Outline width
      },
    })

    const popupTemplate = {
      title: 'Te Pae Christchurch Convention Centre',
      content: 'Where the tech summit is being held',
    }

    // Create a point graphic
    const point = new Point({
      longitude: 172.6358,
      latitude: -43.5292,
    })

    const graphic = new Graphic({
      geometry: point,
      symbol: markerSymbol,
      popupTemplate: popupTemplate,
    })

    // Add the graphic to the graphics layer
    graphicsLayer.add(graphic)
  }
</script>

<main>
  <div class="view" use:createMap />
</main>

<style>
  .view {
    height: 400px;
    width: 800px;
  }
</style>
