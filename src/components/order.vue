<template>
  <div>
    <section class="order__section">
      <order-water class="water" @get-total-cost="getTotalCost"></order-water>
      <order-time class="time" @get-delivery-date="getDeliveryDate"></order-time>
    </section>
    <total-cost :totalCost="totalCost" class="total"></total-cost>
  </div>
</template>

<script>

import OrderWater from './orderWater.vue';
import OrderTime from './orderTime.vue';
import TotalCost from './totalCost.vue';

export default {
  name: 'Order',
  components: {
    OrderWater, OrderTime, TotalCost,
  },
  props: {},
  data() {
    return {
      totalCost: 0,
      isDateDay: null,
      isDateTime: null,
      items: [],
      delivery: {},
    };
  },
  computed: {
    isTotalCost() {
      if (this.totalCost > 0) {
        return true;
      } else {
        return false;
      }
    }
  },
  created() {
  },
  mounted() {},
  methods: {
    getTotalCost(data) {
      this.totalCost = data.data;
      this.items = data.items;
      this.sendOrder();
    },
    getDeliveryDate(data) {
      this.delivery = data.delivery;
      this.isDateDay = data.data.isDateDay;
      this.isDateTime = data.data.isDateTime;
      this.sendOrder();
    },
    sendOrder() {
      let data = new Object();
      data.totalCost = this.totalCost;
      data.isTotalCost = this.isTotalCost;
      data.isDateDay = this.isDateDay;
      data.isDateTime = this.isDateTime;
      this.$emit('get-order', {data: data, items: this.items, delivery: this.delivery});
    },
  },
  watch: {},
};
</script>