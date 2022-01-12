<script>
import Vue from 'vue';
import VueMzcCounter from '@/vue-mzc-counter.vue';
import './serve.css'

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueMzcCounter
  },
  methods: {
    changeCounter(count) {
      console.log(count);
    },
  },
});
</script>

<template>
  <div id="app">
    <vue-mzc-counter :value="2" :max="12" unit="шт" @change="changeCounter" />
  </div>
</template>