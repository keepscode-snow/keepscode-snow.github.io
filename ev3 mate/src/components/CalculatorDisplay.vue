<template>
  <div class="calculator-display">
    {{ value || 0 }}
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  value: {
    type: String,
    required: true
  }
});
</script>

<style scoped>
.calculator-display {
  background-color: gray;
  color: #fff;
  font-size: 2em;
  padding: 0.5em;
  margin-bottom: 1em;

  text-align: right;
  width: 100%;
  border-radius: 10px;
  
}
</style>