<template>
  <div v-if="data !== {}">
    <section class="header">
      <img src="../assets/img/success.png" alt="Order submit" class="header__img">
      <h2 class="header__title">Заказ оформлен</h2>
    </section>
    <section class="order-information">
      <div v-for="item in data.items" :key="item.key" class="order-information__item">
        <span class="order-information__item-left">Бутыль {{item.volume}} л</span>
        <span class="order-information__item-right">{{item.count}} шт.</span>
      </div>
      <div v-if="data.delivery" class="order-information__item">
        <span class="order-information__item-left">День: {{data.delivery.day}}</span>
        <span class="order-information__item-right">Время: {{data.delivery.time}}</span>
      </div>
      <div v-if="data.contacts" class="order-information__item">
        <span class="order-information__item-left">Адрес доставки</span>
        <span class="order-information__item-right">{{data.contacts.adress}}</span>
      </div>
      <div v-if="data.contacts" class="order-information__phone">
        <span class="order-information__item-left">Телефон</span>
        <span class="order-information__item-right">{{data.contacts.phone}}</span>
      </div>
    </section>
    <section class="order-total">
      <h2 class="order-total__header">Итого</h2>
      <span class="order-total__cost">{{data.totalCost}} P</span>
    </section>
    <section class="order-message">
      <p class="order-message__article">Ваш заказ №{{Math.floor(Math.random() * 250)}} успешно оформлен. В ближайшее время по указанному телефону с Вами свяжется наш менеджер.</p>
    </section>
    <section class="order-submit">
      <input type="submit" @click="returnToOrders" class="order-submit__input" value="Новый заказ">
    </section>
  </div>
</template>

<script>

export default {
  name: 'FormConfirmation',
  components: {},
  props: {
    data: Object,
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
    returnToOrders() {
      let formSelector = document.querySelector('.form-selector');
      let formConfirmation = document.querySelector('.form-confirmation');
      formSelector.style.display = 'block';
      formConfirmation.style.display = 'none';
    },
  },
  watch: {},
};
</script>