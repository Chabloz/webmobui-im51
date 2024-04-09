<script setup>
import { ref, computed } from 'vue';

const tempSI = defineModel('tempSI', { type: Number, default: 0 });

const tempCelsius = defineModel('tempCelsius', {
  type: Number,
  default: 0,
  get() {
    return tempSI.value - 273.15;
  },
  set(value) {
    tempSI.value = value + 273.15;
  },
});

const foo = [{name: 'John',  email: 'test@example.com'}, {name: 'Doe'}];

const urlWsSchedule = "https://chabloz.eu/files/horaires/all";
const schedules = ref([]);
fetch(urlWsSchedule)
  .then(response => response.json())
  .then(data => schedules.value = data)
</script>

<template>
  <div>
    <h1>Temperature Converter</h1>
    <input type="number" v-model="tempSI" />
    <input type="number" v-model="tempCelsius" />
  </div>
  <p v-if="tempSI < 0">
    The kelvin is under 0 . Are you sure of the value ?
  </p>
  <p v-else-if="tempSI == 0">
    The kelvin is null.
  </p>
  <p v-else>
    The kelvin is positiv
  </p>
  <p v-show="tempSI < 0">
    The kelvin is under 0 . Are you sure of the value ?
  </p>
  <ul>
    <li v-for="schedule in schedules" :key="item">
      {{ schedule.label }}
    </li>
  </ul>
</template>

<style scoped></style>
