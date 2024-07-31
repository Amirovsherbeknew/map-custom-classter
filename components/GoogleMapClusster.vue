<template>
    <div>
        <gmap-map v-bind:center="center" v-bind:zoom="7" style="width: 100%; height: 500px" @click="placeMarker">
            <gmap-marker v-for="(m, index) in markers" v-bind:position="m.position" v-bind:clickable="true"
                v-bind:draggable="true" @click="center = m.position; showMarkerName(m.name)" v-bind:key="index">
                <div>{{ m.name }}</div>
            </gmap-marker>
        </gmap-map>
        <div v-if="selectedMarker">{{ selectedMarker }}</div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            center: {
                lat: 41.311081,
                lng: 69.240562
            },
            markers: [],
            address: '',
            selectedMarker: ''
        }
    },
    methods: {
        placeMarker(event) {
            const newName = prompt("Joy nomini kiriting:");
            this.markers.push({ name: newName, position: { lat: event.latLng.lat(), lng: event.latLng.lng() } });
            this.center = { lat: event.latLng.lat(), lng: event.latLng.lng() };
        },
        showMarkerName(name) {
            this.selectedMarker = name;
        }
    }
}
</script>
