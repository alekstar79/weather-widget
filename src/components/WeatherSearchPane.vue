<template>
  <h3 class="search-pane__heading">Select the right city</h3>

  <ul class="search-pane__matches">
    <weather-search-result
        @select-result="onSelect"
        v-for="result in searchResults"
        :result="result"
        :key="result.id"
    />
  </ul>
</template>

<script lang="ts">
import { WeatherLocation, WeatherSearchItemNormalized } from '@/weather-api/types'
import WeatherSearchResult from './WeatherSearchResult.vue'
import { defineComponent, PropType } from 'vue'

export default defineComponent({
  components: {
    WeatherSearchResult
  },

  props: {
    searchResults: Array as PropType<WeatherSearchItemNormalized[]>
  },

  emits: ['selectResult'],

  methods: {
    onSelect(e: WeatherLocation) {
      this.$emit('selectResult', e)
    }
  }
})
</script>

<style lang="scss">
@import '../assets/variables';

.search-pane__heading {
  padding: $offset-lg;
  font-size: 0.9rem;
}

.search-pane__matches {
  padding: 0 $offset-lg $offset-lg;
}
</style>
