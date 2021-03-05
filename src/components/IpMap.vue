<template>
    <div id="mapid">
    </div>
    {{ ipGeolocalisation.lat}}
</template>

<script>
import L from 'leaflet';

export default {
  name: 'ipMap',
  data() {
    return {
      map: [],
    };
  },
  props: {
    ipGeolocalisation: {
      lat: Number,
      long: Number,
    },
  },
  watch: {
    ipGeolocalisation(val) {
      console.log('updated');
      this.map.setView([val.lat, val.long]);
      L.marker([val.lat, val.long]).addTo(this.map);
    },
  },
  mounted() {
    const map = L.map('mapid').setView([51.505, -0.09], 13);
    L.tileLayer('https://{s}.tile.openstreetmap.fr/osmfr/{z}/{x}/{y}.png', {
      maxZoom: 19,
      attribution: '&copy; OpenStreetMap France | &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
    })
      .addTo(map);
    this.map = map;
  },
  updated() {
    console.log('updated');
    this.map.setView([this.ipGeolocalisation.lat, this.ipGeolocalisation.long]);
    L.marker([this.ipGeolocalisation.lat, this.ipGeolocalisation.long]).addTo(this.map);
  },
};
</script>
