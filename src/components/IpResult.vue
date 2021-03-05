<template>
  <div class="row search-result-wrapper">
    <div class="row col-8 search-result">
      <div class="col-10 search-result__text-wrapper">
        <p class="search-result__title">ip adress</p>
        <p class="search-result__text">{{ searchResult.ipAddress }}</p>
      </div>
      <div class="col-10 search-result__text-wrapper">
        <p class="search-result__title">location</p>
        <p class="search-result__text">{{ searchResult.ipLocation }}</p>
      </div>
      <div class="col-10 search-result__text-wrapper">
        <p class="search-result__title">timezone</p>
        <p class="search-result__text">{{ searchResult.ipTimezone }}</p>
      </div>
      <div class="col-10 search-result__text-wrapper">
        <p class="search-result__title">isp</p>
        <p class="search-result__text">{{ searchResult.ipIsp }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ipResult',
  props: {
    searchResult: {
      ipAddress: String,
      ipLocation: String,
      ipTimezone: String,
      ipIsp: String,
    },
  },
};
</script>
