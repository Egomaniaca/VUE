<template>
  <div class="home">
    <header>
      <div class="title">My personal costs</div>
      <div >Total price = {{getFullPaymentValue}}</div>
    </header>
    <main>
      <router-link :to="{name: 'AddPaymentForm', params: {section: 'Payment', category: 'Food',},query:{value: 500}}"> Food 500</router-link> <br>
      <router-link :to="{name: 'AddPaymentForm', params: {section: 'Payment', category: 'Food',},query:{value: 100}}"> Food 100</router-link> <br>
      <router-link :to="{name: 'AddPaymentForm', params: {section: 'Payment', category: 'Education',},query:{value: 400}}"> Education 400</router-link><br>
      <router-link :to="{name: 'AddPaymentForm', params: {section: 'Payment', category: 'Education',},query:{value: 300}}"> Education 300</router-link><br>
      <router-link :to="{name: 'AddPaymentForm', params: {section: 'Payment', category: 'Transport',},query:{value: 50}}"> Transport 50</router-link><br>



      <button @click="openModalForm">Show</button>
      <PaymentsDisplay :items="currentElements" />
      <MyPagination :cur="cur" :length="getPaymentsList.length" :n="n" @changePage="changePage" />
    </main>
  </div>
</template>

<script>
import PaymentsDisplay from "@/components/PaymentsDisplay.vue";

import {mapMutations, mapGetters} from "vuex";
import MyPagination from "@/components/MyPagination";


export default {
  name: "HomeView",
  components: {
    PaymentsDisplay,
    MyPagination,
  },
  data() {
    return {
      cur: 1,
      n: 5,
      show: true,
    };

  },
  computed: {
    ...mapGetters(['getFullPaymentValue', 'getPaymentsList']),
    currentElements(){
      return this.getPaymentsList.slice(this.n*(this.cur -1), this.n*(this.cur-1)+this.n)
    }

  },

  methods: {
    ...mapMutations({
      MyMutation: 'setPaymentsListData',
    }),
    addPaymentData(data) {
      this.paymentsList.push(data)
    },
    changePage(p){
      this.cur = p
    },
    openModalForm(){
      this.$modal.show('addform', {title: "AddNewPayment", component: 'AddPaymentForm'})
    }
  },
  created() {
    this.$store.dispatch('fetchData')

  },
  mounted() {
    if(!this.$route.params?.page || isNaN(this.$route.params.page)) return
    this.cur = Number(this.$route.params.page)
  },
};
</script>