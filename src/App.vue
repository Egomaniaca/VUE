<template>
  <div>
    <div class="display">
      <input v-model.number="operand1" />
      <input v-model.number="operand2" />
      = {{result}}
    </div>
    <div class="keyboard">
      <button
          v-for = "operation in operations"
          v-bind:key="operation"
          v-bind:title="operation"
          @click="calculate(operation)">{{operation}}
      </button>
      <div v-show="error">Ошибка! {{ error }}</div>
      <div class="strange-message">
        <template v-if="result < 0">Получилось отрицательное число!</template>
        <template v-else-if="result < 100">Результат в первой сотне</template>
        <template v-else>Получилось слишком большое число</template>
      </div>
      <input v-on:click="visible=!visible" type="checkbox" id="chkKeyboard" value="отобразить экранную клавиатуру" >
      <label for="jack">Отобразить экранную клавиатуру</label>
      <div class="numPad" v-show = "visible">
        <button
            v-for = "button in buttons"
            v-bind:key="button"
            v-bind:title="button"
            @click="writer(button)"
        >{{button}}</button>
        <button @click="delit()">⇚</button>
      </div>
      <br>

      <input name = "chooseOperand" type="radio" id="operand1" value="num1" v-model="a">
      <label for="operand1">Операнд 1</label>
      <input name = "chooseOperand" type="radio" id="operand2" value="num2" v-model="a">
      <label for="operand2">Операнд 2</label>
      <div class="logs">
        <div v-for="(log, id) in logs" v-bind:key="id">{{ log }}</div>
      </div>


    </div>
  </div>
</template>
<script>
import Vue from "vue";

export default {
  name: 'Calculator-fv',
  data(){
    return {
      buttons: ['1','2','3','4','5','6','7','8','9','0',],
      operations:['+', '-', '/', '*','**','(/)>>'],
      result:'',
      operand1: '',
      operand2: '',
      error:'',
      logs: {},
      visible: false,
      a: '0',
    }
  },
  methods: {
    addition(){
      this.result = +this.operand1 + +this.operand2
    },
    subtraction(){
      this.result = this.operand1 - this.operand2
    },
    division(){
        const {operand1, operand2} = this
        if(operand2===0) {
          this.error = 'Делить на 0 нельзя!'
        } else {
          this.result = operand1 / operand2
        }
    },
    multiplicat(){
      this.result = this.operand1 * this.operand2
    },
    exponent(){
      this.result = this.operand1 ** this.operand2
    },
    intDivision(){
      this.result = (this.operand1/this.operand2)>> 0
    },
    calculate (operation = '+') {
      this.error = ''
      switch (operation) {
        case '+':
          this.addition()
          break;
        case '-':
          this.subtraction()
          break;
        case '*':
          this.multiplicat()
          break;
        case '/':
          this.division()
          break;
        case '**':
          this.exponent()
          break;
        case '(/)>>':
          this.intDivision()
          break;
      }

      const key = Date.now()
      const value = `${this.operand1}${operation}${this.operand2}=${this.result}`
      Vue.set(this.logs, key, value)
    },
    writer(Num) {
      if (this.a === "num1") {
        this.operand1 += Num
      }
      if (this.a === "num2") {
        this.operand2  += Num
      }
    },
    delit() {
      let u = 0
      if (this.a === "num1") {
        u = this.operand1 % 10
        this.operand1 -= u
        this.operand1 /= 10
      }
      if (this.a === "num2") {
        u = this.operand2 % 10
        this.operand2 -= u
        this.operand2 /= 10
      }
    }
  }


}
</script>





