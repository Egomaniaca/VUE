<template>
  <div class="home">
    <header>
      <div class="title">My personal costs</div>
      <div >Total price = {{getFullPaymentValue}}</div>
    </header>
    <main>
      <button class="showForm" @click="show = !show">Добавить запись</button>
      <AddPaymentForm v-show="!show" @addNewPayment="addPaymentData" />
      <PaymentsDisplay :items="currentElements" />
      <MyPagination :cur="cur" :length="getPaymentsList.length" :n="n" @changePage="changePage" />
    </main>
  </div>
</template>

<script>
import PaymentsDisplay from "@/components/PaymentsDisplay.vue";
import AddPaymentForm from "@/components/AddPaymentForm.vue";
import {mapMutations, mapGetters} from "vuex";
import MyPagination from "@/components/MyPagination";

export default {
  name: "HomeView",
  components: {
    AddPaymentForm,
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