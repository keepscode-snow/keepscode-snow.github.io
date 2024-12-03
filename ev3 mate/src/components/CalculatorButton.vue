<template>
  <button @click="handleClick" :class="['calculator-button', { 'trig-button': isTrigFunction, 'clear-button': isClearButton }]">
    {{ label }}
  </button>
</template>

<script setup>
import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps({
  label: {
    type: String,
    required: true
  }
});

const emits = defineEmits(['press']);

const handleClick = () => {
  emits('press', props.label);
};

const isTrigFunction = computed(() => ['sin', 'cos', 'tan'].includes(props.label));
const isClearButton = computed(() => props.label === 'C');
</script>

<style scoped>
.calculator-button {
  background: #444;
  border: none;
  color: #fff;
  font-size: 1.5em;
  margin: 0.2em;
  padding: 1em;
  width: 3em;
  height: 3em;
}

.trig-button {
  background: #008080;
}

.clear-button {
  background: #f00;
}
</style>