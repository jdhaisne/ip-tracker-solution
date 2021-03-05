<template>
  <div class="container">
    <div class="row header">
        <div class="col-xs-11 col-md-12 mx-a">
          <trackerHeader
          :ipAddress="ipAddress"
          :searchResult="searchResult"
          @updateIpAddress="updateIpAddress"
          @searchIp="searchIp"
          >
          </trackerHeader>
          <ipMap
          :ipGeolocalisation="ipGeolocalisation">
          </ipMap>
        </div>
      </div>
  </div>
</template>

<script>
import trackerHeader from '@/components/TrackerHeader.vue';
import ipMap from '@/components/IpMap.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    trackerHeader,
    ipMap,
  },
  data() {
    return {
      ipAddress: '',
      searchResult: {
        ipAddress: '-',
        ipLocation: '-',
        ipTimezone: '-',
        ipIsp: '-',
      },
      ipGeolocalisation: {
        lat: 0,
        long: 0,
      },
    };
  },
  methods: {
    updateIpAddress(value) {
      this.ipAddress = value;
    },
    searchIp() {
      const ipifyUrl = process.env.VUE_APP_IPIFY_URL;
      const APIKey = process.env.VUE_APP_IPIFY_API_KEY;
      axios.get(ipifyUrl, {
        params: {
          apiKey: APIKey,
          ipAddress: this.ipAddress,
        },
      })
        .then((response) => {
          console.log(response);
          this.searchResult.ipAddress = response.data.ip;
          this.searchResult.ipLocation = `${response.data.location.city}, ${response.data.location.region} ${response.data.location.postalCode}`;
          this.searchResult.ipTimezone = `UTC ${response.data.location.timezone}`;
          this.searchResult.ipIsp = response.data.isp;
          this.ipGeolocalisation.lat = response.data.location.lat;
          this.ipGeolocalisation.long = response.data.location.lng;
        })
        .catch((error) => {
          console.log(error);
        })
        .then(() => {
          console.log('done');
        });
    },
  },
};
</script>
