<template>
<h1>Vuelculator</h1>

  <div class="calc">
    <div class="display">
      {{ equation }}
    </div>

    <div class="keypad">

      <div class="key" @click="useNumber(1)">1</div>
      <div class="key" @click="useNumber(2)">2</div>
      <div class="key" @click="useNumber(3)">3</div>
      <div class="key" @click="plus()">+</div>

      <div class="key" @click="useNumber(4)">4</div>
      <div class="key" @click="useNumber(5)">5</div>
      <div class="key" @click="useNumber(6)">6</div>
      <div class="key" @click="minus()">-</div>

      <div class="key" @click="useNumber(7)">7</div>
      <div class="key" @click="useNumber(8)">8</div>
      <div class="key" @click="useNumber(9)">9</div>
      <div class="key" @click="multiply()">x</div>

      <div class="key" @click="clear()">AC</div>
      <div class="key" @click="useNumber(0)">0</div>
      <div class="key" @click="divide()">/</div>
      <div class="key" @click="result()">=</div>

    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  const equation = ref('0');
  /**
   * @description This function concatenates a number to the equation
   * @param { Number } num => number to be added to equation
  **/
  const useNumber = (num) => {
    equation.value = !!parseInt(equation.value) ? `${equation.value}` + `${num}` : `${num}`;
  };
  const plusOperator = ' + ';
  /**
   * @description This function concatenates a plus sign to the equation
  **/
  const plus = () => {
    equation.value = `${checkOperator(equation.value, plusOperator)}` + plusOperator;
  }
  const minusOperator = ' - ';
  /**
   * @description This function concatenates a minus sign to the equation
  **/
  const minus = () => {
    equation.value = `${checkOperator(equation.value, minusOperator)}` + minusOperator;
  }
  const multiplyOperator = ' x ';
  /**
   * @description This function concatenates a multiplication sign(x) to the equation
  **/
  const multiply = () => {
    equation.value = `${checkOperator(equation.value, multiplyOperator)}` + multiplyOperator;
  }
  const divideOperator = ' / ';
  /**
   * @description This function concatenates a division sign to the equation
  **/
  const divide = () => {
    equation.value = `${checkOperator(equation.value, divideOperator)}` + divideOperator;
  }
  /**
   * @description This function clears the equation
  **/
  const clear = () => { equation.value = '0'}
  /**
   * @description This function checks for an operator at the end of the equation and replaces it with the one concatenated last
  **/
  const checkOperator = (equation, requestedOperator) => {
    console.log("equation --- ", equation)
    return equation.replace(/( [\+\-\/x] )$/g, '')
  }
  /**
   * @description This function resolves the equation to give a mathematical answer
  **/
  const result = () => {
    let eqResult = Function('"use strict";return (' + equation.value.replace(/( \x+ )/g, ' * ') + ')')();
    equation.value = `${eqResult}`;
  }
</script>

<style scoped>
@font-face {
  font-family: "digital";
  src: local("digital"),
  url("./fonts/digital-7/digital-7.ttf");
}
.calc{
  width: 320px;
  height: 480px;
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background-color: grey;
  border: 2px solid teal;
}

.display{
  flex: 1;
  background-color: #607d8b;
  margin: 10px;
  font-size: 40px;
  text-align: right;
  overflow-wrap: break-word;
  padding: 5px;
  font-family: "digital";
}

.keypad{
  height: 320px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 4px;
}

.key{
  display: flex;
  background-color: #009688;
  justify-content: center;
  align-items: center;
  font-size: 40px;
  color: black;
  cursor: pointer;
}
::selection{
  background: none;
}
</style>
