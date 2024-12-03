<template>
  <div class="calculator">
    <CalculatorDisplay :value="displayValue" />
    <div class="calculator-buttons">
      <CalculatorButton v-for="button in buttons" :key="button" :label="button" @press="handleButtonPress" />
    </div>
    <div class="decimal-control">
      <label for="decimals">Decimales:</label>
      <input type="number" id="decimals" v-model="decimalPlaces" min="0" max="10" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import CalculatorDisplay from './CalculatorDisplay.vue';
import CalculatorButton from './CalculatorButton.vue';

const displayValue = ref('');
const decimalPlaces = ref(2); // Número de decimales por defecto
const buttons = [
  'sin', 'cos', 'tan', '(', ')',
  '7', '8', '9', '/', '*',
  '4', '5', '6', '-', '+',
  '1', '2', '3', '.', '0',
  'C', '=', '←'
];

const handleButtonPress = (label) => {
  if (label === 'C') {
    displayValue.value = '';
  } else if (label === '=') {
    try {
      const result = eval(displayValue.value);
      displayValue.value = result.toFixed(decimalPlaces.value).toString();
    } catch (e) {
      displayValue.value = 'Error';
    }
  } else if (label === 'sin') {
    displayValue.value = Math.sin(parseFloat(displayValue.value)).toFixed(decimalPlaces.value).toString();
  } else if (label === 'cos') {
    displayValue.value = Math.cos(parseFloat(displayValue.value)).toFixed(decimalPlaces.value).toString();
  } else if (label === 'tan') {
    displayValue.value = Math.tan(parseFloat(displayValue.value)).toFixed(decimalPlaces.value).toString();
  } else if (label === '←') {
    displayValue.value = displayValue.value.slice(0, -1);
  } else {
    displayValue.value += label;
  }
};
</script>

<style scoped>
.calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 2em;
  background-color: black;
}

.calculator-buttons {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0.5em;
}

.decimal-control {
  margin-top: 1em;
  display: flex;
  align-items: center;
}

.decimal-control label {
  margin-right: 0.5em;
}
</style>