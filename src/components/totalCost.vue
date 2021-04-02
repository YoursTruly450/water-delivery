<template>
  <div>
    <h2 class="total__header">Итого</h2>
    <span class="total__cost">{{totalCost}} P</span>
  </div>
</template>

<script>

export default {
  name: 'TotalCost',
  components: {},
  props: {
    totalCost: Number,
  },
  data() {
    return {};
  },
  computed: {
  },
  created() {
  },
  mounted() {},
  methods: {
  },
  watch: {},
};
</script>