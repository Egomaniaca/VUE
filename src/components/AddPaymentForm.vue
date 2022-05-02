<template>
  <div class="form-wrapper">
    <input v-model="date" placeholder="Дата">
    <input v-model="category" placeholder="Категория"/>
    <input v-model="value" placeholder="Сумма"/>
    <button @click="onClickSave">Сохранить</button>
  </div>
</template>
<script>
  export default {
    name: "AddPaymentForm",
    date() {
      return {
        date: "",
        category: "",
        value: ""
      }
    },
    computed: {
      getCurrentDate() {
        const today = new Date()
        const formater = new Intl.DateTimeFormat("ru",{

          year: "numeric",
          month: "long",
          day: "numeric"
        });
       /* const d = today.getDate()
        const m = today.getMonth() + 1
        const y = today.getFullYear()*/
        return formater.format(today)
      }
    },
    methods: {
      onClickSave() {
        const data = {
          date: this.date || this.getCurrentDate,
          category: this.category,
          value: this.value
        }
        this.$emit('addNewPayment', data)
        console.log(data);
      }
    },
  }
</script>