<script setup>
  import { ref } from 'vue';
  import BaseInputNumber from './components/BaseInputNumber.vue';

  const tempSI = ref(0); //  kelvin

  const tempCelsius = defineModel('celsius', {
    get() {
      return tempSI.value - 273.15;
    },
    set(val) {
      tempSI.value = val + 273.15;
    }
  });

  const tempKelvin = defineModel('kelvin', {
    get() {
      return tempSI.value;
    },
    set(val) {
      tempSI.value = val;
    }
  });

  const tempFahrenheit = defineModel('fahrenheit', {
    get() {
      return (tempSI.value - 273.15) * 9 / 5 + 32;
    },
    set(val) {
      tempSI.value = (val - 32) * 5 / 9 + 273.15;
    }
  });
</script>

<template>

  <BaseInputNumber
    unit="°C"
    v-model="tempCelsius"
  />
  <BaseInputNumber
    unit="°F"
    v-model="tempFahrenheit"
  />
  <BaseInputNumber
    unit="K"
    v-model="tempKelvin"
    :decimal-places="2"
    step="0.01"
    min="0"
    id="kelvin"
  />

</template>

<style scoped>

</style>
