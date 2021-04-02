<template>
  <div>
    <h2 class="time__header">Дата и время доставки</h2>
    <section class="time__day">
      <h3 class="time__subheader">день</h3>
      <div class="time__day-selector">
        <img class="time__img_arrows" src="../assets/img/arrow_left.svg" alt="left arrow" @click="minusDay">
        <div v-for="day in days" :key="day.weekDay" class="time__selector-form">
          <input :id="day.weekDay" type="radio" class="time__selector-input"
          v-model="selectedDay" :value="day" @click="selectDay(day)">
          <label class="time__label-no-text" :for="day.weekDay"></label>
          <label class="time__label-day" :for="day.weekDay">{{day.day}}</label>
          <label class="time__label-weekday" :for="day.weekDay">{{day.weekDay}}</label>
        </div>
        <img class="time__img_arrows" src="../assets/img/arrow_right.svg" alt="right arrow" @click="plusDay">
      </div>
    </section>
    <section class="time__day-time">
      <h3 class="time__subheader">время</h3>
      <div v-if="times.length > 0" class="time__hours-selector">
        <div v-for="time in times" :key="time" class="time__hours-form">
          <input :id="time" type="radio" class="time__input-hours"
          v-model="selectedTime" :value="time" @click="selectTime(time)">
          <label class="time__label-hours" :for="time">{{time}}</label>
        </div>
      </div>
      <div v-else class="time__hours-selector">
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'OrderTime',
  components: {
  },
  props: {},
  data() {
    return {
      days: [],
      weekDays: ['ВС', 'ПН', 'ВТ', 'СР', 'ЧТ', 'ПТ', 'СБ'],
      selectedDay: {},
      times: [],
      selectedTime: null,
    };
  },
  computed: {
  },
  created() {
  },
  mounted() {
    this.daysInit();
  },
  methods: {
    daysInit() {
      let date = new Date();
      this.days.push(this.dayObject(date));
      for (let i = 1; i < 7; i++) {
        date.setDate(date.getDate() + 1);
        this.days.push(this.dayObject(date));
      }
    },
    dayObject(date) {
      let item = new Object();
      item.date = String(date);
      item.stringDate = date.toLocaleString('RU').split(',')[0];
      item.day = item.stringDate.split('.')[0];
      item.weekDay = this.weekDays[date.getDay()];
      return item;
    },
    selectDay(day) {
      if (day.weekDay === 'ВС' || day.weekDay === 'СБ') {
        this.times = ['12:00 - 13:00', '15:00 - 16:00'];
      } else {
        this.times = ['10:00 - 11:00', '12:00 - 13:00', '15:00 - 16:00'];
      }
      this.selectedDay = day;
      this.selectedTime = null;
      this.sendTime();
    },
    minusDay() {
      let minDate = new Date();
      let curDate = new Date(this.days[0].date);
      if (minDate < curDate) {
        this.days = this.days.map((el) => {
          let date = new Date(el.date);
          date.setDate(date.getDate() - 1);
          return el = this.dayObject(date);
        });
      }
    },
    plusDay(){
      this.days = this.days.map((el) => {
        let date = new Date(el.date);
        date.setDate(date.getDate() + 1);
        return el = this.dayObject(date);
      });
    },
    selectTime(time){
      this.selectedTime = time;
      this.sendTime();
    },
    sendTime() {
      let data = new Object();
      let delivery = new Object();
      delivery.day = this.selectedDay.stringDate;
      delivery.time = this.selectedTime;
      data.isDateDay = this.selectedDay === {} ? false : true;
      data.isDateTime = this.selectedTime === null ? false : true;
      this.$emit('get-delivery-date', {data: data, delivery: delivery});
    }
  },
  watch: {},
};
</script>