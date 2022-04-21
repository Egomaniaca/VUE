<template>
  <div>
    <div class="display">
      <input v-model="operand1"/>
      <input v-model="operand2"/>
      = {{result}}
    </div>
    <div class="keyboard">
      <button @click="result = +operand1 + +operand2">+</button> 
      <button @click="result = +operand1 - +operand2">-</button>
      <button @click="result = +operand1 / +operand2">/</button>
      <button @click="result = +operand1 * +operand2">*</button>
      <button @click="result = operand1 ** operand2">Возведение в степень</button>
      <button @click="result = (operand1 / operand2) >> 0 ">Целочисленное деление</button>

    </div>
  </div>
</template>
<script>
export default {
  name: 'Calculator-fv',
  data(){
    return {
      operand1: '',
      operand2: '',
      result: ''
    }
  }
}
</script>





