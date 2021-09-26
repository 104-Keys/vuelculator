<template>
<h1>Vuelculator</h1>

  <div class="calc">
    <div class="display">
    </div>

    <div class="keypad">

      <div class="key">1</div>
      <div class="key">2</div>
      <div class="key">3</div>
      <div class="key">+</div>

      <div class="key">4</div>
      <div class="key">5</div>
      <div class="key">6</div>
      <div class="key">-</div>

      <div class="key">7</div>
      <div class="key">8</div>
      <div class="key">9</div>
      <div class="key">x</div>

      <div class="key">AC</div>
      <div class="key">0</div>
      <div class="key">/</div>
      <div class="key">=</div>

    </div>
  </div>
</template>

<script setup>
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
