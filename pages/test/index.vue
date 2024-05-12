<template>
    <div>{{ center }} {{ markers }}
        <gmap-map v-bind:center="center" v-bind:zoom="7" style="width: 100%; height: 500px">
            <gmap-cluster>
                <gmap-marker v-for="(m, index) in markers" v-bind:position="m.position" v-bind:clickable="true"
                    v-bind:draggable="true" @click="center = m.position" v-bind:key="index"></gmap-marker>
            </gmap-cluster>
        </gmap-map>
    </div>
</template>
<script>
export default {
    data() {
        return {
            center: {
                lat: 10.0,
                lng: 10.0
            },
            markers: [{
                position: {
                    lat: 10.0,
                    lng: 10.0
                }
            }, {
                position: {
                    lat: 11.0,
                    lng: 11.0
                }
            }]
        }
    }
}
</script>
<!-- 2cd4b97d-110c-47bb-a70c-561731a8b380 -->