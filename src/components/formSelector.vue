<template>
    <div>
      <contacts class="contacts" @get-contacts="getContacts"></contacts>
      <order class="order" @get-order="getOrder"></order>
      <section class="submit">
        <input type="submit" @click="submitOrder" class="submit__input" value="Заказать воду">
        <span class="submit__message">{{message}}</span>
      </section>
    </div>
</template>

<script>

import Order from './order.vue';
import Contacts from './contacts.vue';

export default {
    name: 'FormSelector',
    components: {
      Order, Contacts,
    },
    props: {},
    data() {
        return {
          isTotalCost: null,
          isName: null,
          isPhone: null,
          isMail: null,
          isAdress: null,
          isChecked: null,
          isDateDay: null,
          isDateTime: null,
          message: '',
          conacts: {},
          delivery: {},
          items: [],
          totalCost: 0,
        };
    },
    computed: {
    },
    created() {
    },
    mounted() {},
    methods: {
      getContacts(data) {
        this.contacts = data.contacts;
        this.isName = data.data.isName;
        this.isMail = data.data.isMail;
        this.isPhone = data.data.isPhone;
        this.isAdress = data.data.isAdress;
        this.isChecked = data.data.isChecked;
      },
      getOrder(data){
        this.delivery = data.delivery;
        this.items = data.items;
        this.totalCost = data.data.totalCost;
        this.isTotalCost = data.data.isTotalCost;
        this.isDateDay = data.data.isDateDay;
        this.isDateTime = data.data.isDateTime;
      },
      submitOrder(){
        if (!this.isName) {
          this.message = 'Заполните корректно имя';
        } else if(!this.isMail) {
          this.message = 'Заполните корректно e-mail';
        } else if(!this.isPhone) {
          this.message = 'Заполните корректно телефон';
        } else if(!this.isAdress) {
          this.message = 'Заполните корректно адрес';
        } else if(!this.isChecked) {
          this.message = 'Подтвердите согласие на обработку персональных данных';
        } else if(!this.isDateDay) {
          this.message = 'День доставки не выбран';
        } else if(!this.isDateTime) {
          this.message = 'Время доставки не выбрано';
        } else if(!this.isTotalCost) {
          this.message = 'Вы ничего не заказали';
        } else {
          this.message = 'Заказ успешно оформлен';
          let data = new Object();
          data.totalCost = this.totalCost;
          data.delivery = this.delivery;
          data.contacts = this.contacts;
          data.items = this.items;
          this.$emit('get-data', {data: data});
          let formSelector = document.querySelector('.form-selector');
          let formConfirmation = document.querySelector('.form-confirmation');
          formSelector.style.display = 'none';
          formConfirmation.style.display = 'block';
        }
      },
    },
    watch: {},
};
</script>