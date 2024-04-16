<script setup>
  import { ref, computed } from 'vue';
  import scheduleData from './mock/schedule.json';

  const schedule = ref(scheduleData);

  const scheduleOrderByDate = computed(() => {
    return schedule.value.sort((a, b) => {
      return new Date(a.start) - new Date(b.start);
    });
  });

  const showHistory = ref(false);

  const scheduleFiltered = computed(() => {
    if (showHistory.value) {
      return scheduleOrderByDate.value;
    }
    return scheduleOrderByDate.value.filter((item) => {
      return new Date(item.start) > new Date();
    });
  });

</script>

<template>
  <div>
    <h1>App Schedule</h1>
    <button @click="showHistory = !showHistory">
      {{ showHistory ? 'Hide' : 'Show' }} History
    </button>
    <ul>
      <li v-for="item in scheduleFiltered" :key="item.id">
        {{ item.start }} {{ item.label }}
      </li>
    </ul>
  </div>

</template>

<style scoped>

</style>