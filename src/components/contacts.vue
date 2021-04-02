<template>
    <div>
      <h2 class="contacts__header">Заполните данные</h2>
      <section class="contacts__data">
        <input class="contacts__input" type="text" placeholder="Имя" v-model="name" @input="sendContacts" pattern="^[а-яёА-ЯЁa-zA-z -]+$">
        <input class="contacts__input" type="text" placeholder="e-mail" v-model="mail" @input="sendContacts" pattern="^[-\w.]+@([A-z0-9][-A-z0-9]+\.)+[A-z]{2,4}$">
        <input class="contacts__input" type="text" placeholder="Телефон" v-model="phone" @input="sendContacts" pattern="^(\+7|7|8)?[\s-]?\(?[489][0-9]{2}\)?[\s-]?[0-9]{3}[\s-]?[0-9]{2}[\s-]?[0-9]{2}$">
        <input class="contacts__input" type="text" placeholder="Адрес" v-model="adress" @input="sendContacts" patter="^[а-яёА-ЯЁa-zA-Z0-9 ,.-]{7,}">
        <div class="contacts__input-group">
          <input class="contacts__checkbox" type="checkbox" v-model="isCheckedPersonalData" @change="toggleChecked">
          <span class="contacts__traitement">Я согласен на 
            <a 
            href="https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D1%81%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5">
            обработку персональных данных</a></span>
        </div>
      </section>
    </div>
</template>

<script>

export default {
    name: 'Contacts',
    components: {},
    props: {},
    data() {
        return {
          name: '',
          phone: '',
          adress: '',
          mail: '',
          isCheckedPersonalData: null,
        };
    },
    computed: {
      isChecked() {
        if (this.isCheckedPersonalData) {
          return true;
        } else {
          return false;
        }
      },
      isName() {
        if (/^[а-яёa-z -]+$/i.test(this.name)) {
          return true;
        } else {
          return false;
        }
      },
      isAdress() {
        if (/^[а-яёa-z0-9 ,.-]+$/i.test(this.adress)) {
          return true;
        } else {
          return false;
        }
      },
      isMail() {
        if (/^[-\w.]+@([A-z0-9][-A-z0-9]+\.)+[A-z]{2,4}$/i.test(this.mail)) {
          return true;
        } else {
          return false;
        }
      },
      isPhone() {
        if (/^(\+7|7|8)?[\s-]?\(?[489][0-9]{2}\)?[\s-]?[0-9]{3}[\s-]?[0-9]{2}[\s-]?[0-9]{2}$/i.test(this.phone)) {
          return true;
        } else {
          return false;
        }
      },
    },
    created() {
    },
    mounted() {},
    methods: {
      toggleChecked() {
        this.sendContacts();
      },
      sendContacts() {
        let contacts = new Object();
        let data = new Object();
        contacts.name = this.name;
        contacts.mail = this.mail;
        contacts.phone = this.phone;
        contacts.adress = this.adress;
        data.isName = this.isName;
        data.isMail = this.isMail;
        data.isPhone = this.isPhone;
        data.isAdress = this.isAdress;
        data.isChecked = this.isChecked;
        this.$emit('get-contacts', {data: data, contacts: contacts});
      },
    },
    watch: {},
};
</script>