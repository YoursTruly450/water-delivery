<template>
  <div>
    <clean-water class="clean-water"></clean-water>
    <form-selector class="form-selector" @get-data="dataLoad"></form-selector>
    <form-confirmation :data="data" class="form-confirmation"></form-confirmation>
  </div>
</template>

<script>

import CleanWater from './cleanWater.vue';
import FormSelector from './formSelector.vue';
import FormConfirmation from './formConfirmation.vue';

export default {
  name: 'MainPage',
  components: {
    CleanWater, FormSelector, FormConfirmation,
  },
  props: {},
  data() {
    return {
      data: {},
    };
  },
  computed: {
  },
  created() {
  },
  mounted() {},
  methods: {
    dataLoad(data) {
      this.data = data.data;
    },
  },
  watch: {},
};
</script>