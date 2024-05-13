<!-- Please remove this file from your project -->
<template>
  <div id="map"></div>
</template>

<script>
export default {
  name: 'NuxtTutorial',
  data () {
    return {
       triangleCoords: [
      { lat: 25.774, lng: -80.19 },
      { lat: 18.466, lng: -66.118 },
      { lat: 32.321, lng: -64.757 },
      { lat: 25.774, lng: -80.005 },
      { lat: 25.704, lng: -80.02 },
      { lat: 25.674, lng: -80.05 },
      { lat: 25.744, lng: -80.01 },
      { lat: 25.714, lng: -79.004 },
      { lat: 25.714, lng: -79.005 },
      { lat: 25.714, lng: -79.23 },
      { lat: 25.214, lng: -79.23 },
      { lat: 25.214, lng: -79.23 },
      { lat: 25.114, lng: -79.23 },
      { lat: 25.314, lng: -79.023 },
      { lat: 25.514, lng: -79.004 },
      { lat: 25.613, lng: -79.123 },
      { lat: 25.732, lng: -79.003 },
      { lat: 25.724, lng: -79.213 },
      { lat: 25.767, lng: -79.223 },
      { lat: 25.785, lng: -79.233 },
      { lat: 25.714, lng: -79.213 },
      { lat: 25.743, lng: -79.233 },
      { lat: 25.705, lng: -79.001 },
      { lat: 25.775, lng: -79.223 },
      { lat: 25.760, lng: -79.002 },
      { lat: 25.709, lng: -79.223 },
      { lat: 25.708, lng: -79.123 },
      { lat: 25.707, lng: -79.132 },
      { lat: 25.705, lng: -79.232 },
      { lat: 25.754, lng: -79.201 }
    ],
    map:null
    }
  },
  mounted() {
     this.initializationCallback()
  },
  methods:{
    initializationCallback () {
      this.map = new google.maps.Map(document.getElementById('map'), {
      center: { lat: 41.8781, lng: -87.6298 },
      zoom: 8
    });

    // Polygonni yaratish

    const polygon = new google.maps.Polygon({
      paths: this.triangleCoords,
      strokeColor: '#fc1703',
      strokeOpacity: 0.8,
      strokeWeight: 2,
      fillColor: '#FF0000',
      fillOpacity: 0.35
    });
    
    polygon.setMap(this.map);      
    }
  }

}
</script>
<style>
#map {
  height: 400px;
  width: 100%;
}
</style>