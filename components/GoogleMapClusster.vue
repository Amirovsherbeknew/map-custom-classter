<template>
    <div>
        <gmap-map v-bind:center="center" v-bind:zoom="7" style="width: 100%; height: 500px" @click="placeMarker">
            <gmap-marker v-for="(m, index) in markers" v-bind:position="m.position" v-bind:clickable="true"
                v-bind:draggable="true" @click="center = m.position" v-bind:key="index">
                <div>{{ m.name }}</div>
            </gmap-marker>
        </gmap-map>
        <input type="text" v-model="address" placeholder="Manzil kiriting">
        <button @click="geocodeAddress">Qidirish</button>
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
            address: ''
        }
    },
    methods: {
        placeMarker(event) {
            const newName = prompt("Joy nomini kiriting:");
            this.markers.push({ name: newName, position: { lat: event.latLng.lat(), lng: event.latLng.lng() } });
            this.center = { lat: event.latLng.lat(), lng: event.latLng.lng() };
        },
        geocodeAddress() {
            const geocoder = new google.maps.Geocoder();
            geocoder.geocode({ address: this.address }, (results, status) => {
                if (status === 'OK') {
                    const location = results[0].geometry.location;
                    const newName = prompt("Joy nomini kiriting:");
                    this.markers.push({ name: newName, position: { lat: location.lat(), lng: location.lng() } });
                    this.center = { lat: location.lat(), lng: location.lng() };
                } else {
                    alert('Manzil topilmadi: ' + status);
                }
            });
        }
    }
}
</script>
