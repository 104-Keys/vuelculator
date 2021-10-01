<template>
  <div class="calc">
    <div class="display">
      {{ equation }}
    </div>

    <div class="keypad">

      <div class="key num" @click="useNumber(1)">1</div>
      <div class="key num" @click="useNumber(2)">2</div>
      <div class="key num" @click="useNumber(3)">3</div>
      <div class="key fn" @click="plus()">+</div>

      <div class="key num" @click="useNumber(4)">4</div>
      <div class="key num" @click="useNumber(5)">5</div>
      <div class="key num" @click="useNumber(6)">6</div>
      <div class="key fn" @click="minus()">-</div>

      <div class="key num" @click="useNumber(7)">7</div>
      <div class="key num" @click="useNumber(8)">8</div>
      <div class="key num" @click="useNumber(9)">9</div>
      <div class="key fn" @click="multiply()">x</div>

      <div class="key special" @click="clear()">AC</div>
      <div class="key num" @click="useNumber(0)">0</div>
      <div class="key fn" @click="divide()">/</div>
      <div class="key fn" @click="result()">=</div>

    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  const equation = ref('0');
  let resultCalled = ref(false);
  let lastResult = ref(0);
  /**
   * @description This function concatenates a number to the equation
   * @param { Number } num => number to be added to equation
  **/
  const useNumber = (num) => {
    equation.value = resultCalled.value ? `${num}` : (!!parseInt(equation.value) ? `${equation.value}` + `${num}` : (equation.value.search(/^[\-]$/g) !== -1 ? `${equation.value}` + `${num}` : `${num}`));
    resultCalled.value = false;
  };
  const plusOperator = ' + ';
  /**
   * @description This function concatenates a plus sign to the equation
  **/
  const plus = () => {
    equation.value = `${checkOperator(equation.value, plusOperator)}`;
  }
  const minusOperator = ' - ';
  /**
   * @description This function concatenates a minus sign to the equation
  **/
  const minus = () => {
    equation.value = `${checkOperator(equation.value, minusOperator)}`;
  }
  const multiplyOperator = ' x ';
  /**
   * @description This function concatenates a multiplication sign(x) to the equation
  **/
  const multiply = () => {
    equation.value = `${checkOperator(equation.value, multiplyOperator)}`;
  }
  const divideOperator = ' / ';
  /**
   * @description This function concatenates a division sign to the equation
  **/
  const divide = () => {
    equation.value = `${checkOperator(equation.value, divideOperator)}`;
  }
  /**
   * @description This function clears the equation
  **/
  const clear = () => { equation.value = '0'}
  /**
   * @description This function checks for an operator at the end of the equation and replaces it with the one concatenated last
  **/
  const checkOperator = (equation, requestedOperator) => {
    return equation.search(/^0$/g) !== -1 ? (requestedOperator.search(/( [\/x] )$/g) !== -1 ? '0' : requestedOperator.replace(/ /g, '')) : equation.replace(/( [\+\-\/x] )$/g, '') + requestedOperator;
    /* equation.value = resultCalled.value ? lastResult + `${checkOperator(equation.value, plusOperator)}` : ;
    resultCalled.value = false; */
  }
  /**
   * @description This function resolves the equation to give a mathematical answer
  **/
  const result = () => {
    let finalEqn = equation.value.replace(/( [\+\-\/x] )$/g, '')
    resultCalled.value = finalEqn.search(/( [\+\-\/x] )/g) !== -1
    let eqResult = Function('"use strict";return (' + finalEqn.replace(/( \x+ )/g, ' * ') + ')')();
    equation.value = `${eqResult}`;
    lastResult.value = eqResult;
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
  background-color: #D9D3C7;
  border: 2px solid #D9D3C7;
}

.display{
  flex: 1;
  background-color: #A5B3A6;
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
  gap: 8px;
  margin: 10px;
}

.key{
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 40px;
  cursor: pointer;
}
.num{
  background-color: #525759;
  color: #ffffff;
}
.fn{
  background-color: #877569;
  color: #000000;
}
.special{
  background-color: #BD5A04;
  color: #000000;
  font-size: 35px;
  font-weight: bold;
}
::selection{
  background: none;
}
</style>
