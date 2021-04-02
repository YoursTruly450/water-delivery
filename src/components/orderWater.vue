<template>
    <div>
      <h2 class="water__header">Вода</h2>
      <section v-if="isChecked" class="water__section">
        <div v-for="bottle in bottles" :key="bottle.key" class="water__input-group">
          <img class="water__img" :src="require( `../assets/img/${bottle.img}` )" alt="Bottle of water">
          <label class="water__volume">{{bottle.volume}} л</label>
          <label class="water__rest">{{bottle.count}} шт</label>
          <label class="water__cost">{{bottle.cost}} Р</label>
          <input class="water__input" type="radio"
          v-model="selectedBottle" v-bind:value="bottle">
          <div v-if="bottle.checked" class="water__submit">
            <img src="../assets/img/btn_minus.png" alt="minus button" @click="removeBottle(bottle)">
            <span class="water__counter">{{bottle.count}}</span>
            <img src="../assets/img/btn_plus.png" alt="plus button" @click="addBottle(bottle)">
          </div>
          <div v-else class="water__submit">
          </div>
        </div>
      </section>
    </div>
</template>

<script>

export default {
    name: 'OrderWater',
    components: {},
    props: {},
    data() {
        return {
          bottles: [
            {key: 0, img: 'water_large.png', cost: 220, volume: 18.9, count: 0, checked: false},
            {key: 1, img: 'water_small.png', cost: 175, volume: 1.5, count: 0, checked: false},
            {key: 2, img: 'water_small.png', cost: 270, volume: 0.5, count: 0, checked: false},
          ],
          selectedBottle: {},
        };
    },
    computed: {
      isChecked() {
        let isChecked = this.bottles.map((el) => this.selectedBottle.volume === el.volume);
        isChecked.forEach((el, index) => {
          this.bottles[index].checked = el;
        });
        return isChecked;
      },
    },
    created() {
    },
    mounted() {},
    methods: {
      removeBottle(item) {
        let index = item.key;
        if (this.bottles[index].count > 0) {
          this.bottles[index].count--;
        }
        this.totalCostCalculate();
      },
      addBottle(item) {
        let index = item.key;
        this.bottles[index].count++;
        this.totalCostCalculate();
      },
      totalCostCalculate() {
        let bottles = this.bottles.filter((el) => el.count > 0);
        let totalCost = 0;
        this.bottles.forEach((el) => {
          totalCost += el.cost * el.count;
        });
        this.$emit('get-total-cost', {data: totalCost, items: bottles});
      }
    },
    watch: {},
};
</script>