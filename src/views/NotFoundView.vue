<template>
  <div class="about">
    <h1>This is an NotFound page</h1>
    <button @click="openModalAuthForm">Show</button>
  </div>
</template>

<script>
export default {
  name: "NotFound",
  methods:{
    openModalAuthForm(){
      this.$modal.show('auth',{title: 'Auth-Form', component: 'auth'})
    }
  }
}
</script>