<template>
  <div id="app">
    <nav>
      <router-link to="/dashboard">Dashboard</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/notFound">Not Found</router-link>
    </nav>

    <ModalWindowAddPaymentForm :settings="settings" v-if="modalShow"/>

    <img alt="politCat" src="./assets/politcat.png">
    <router-view/>
    <Transition
        name="custom-classes"
        enter-active-class="animate__animated animate__tada"
        leave-active-class="animate__animated animate__bounceOutRight"
    >
     <ModalWindowAddPaymentForm :settings="settings"  v-if="modalShow"/>
    </Transition>
    <Transition
        name="custom-classes"
        enter-active-class="animate__animated animate__tada"
        leave-active-class="animate__animated animate__bounceOutRight"
    >
      <ContextMenu/>
    </Transition>
  </div>
</template>

<script>



import ContextMenu from "@/components/ContextMenu";
export default {
  data(){
    return {
      modalShow: false,
      settings: {}
    }
  },
  name: 'App',

  methods:{
    onShow(data){
      this.modalShow = true
      this.settings = data
      console.log(data)
    },
    onHide(){
      this.settings = {}
        this.modalShow = false

    }


  },
  mounted() {
    this.$modal.EventBus.$on('show',this.onShow)
    this.$modal.EventBus.$on('hide',this.onHide)
  },
  beforeDestroy() {
    this.$modal.EventBus.$off('show',this.onShow)
    this.$modal.EventBus.$off('hide',this.onHide)
  },
  components: {
    ContextMenu,
    ModalWindowAddPaymentForm:()=> import('./components/ModalWindowAddPaymentForm')
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h1{
  font-size: 50px;
}
nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css";

</style>