<script setup lang="ts">
import JobListComponent from '@/components/JobListComponent.vue';
import { ref } from 'vue';
import type Job from './types/job';
import type OrderTerm from './types/OrderTerm';

const jobs = ref<Job[]>([
  { title: 'farm worker', location: 'near ranch', salary: 3500, id: '1' },
  { title: 'school teacher', location: 'Camil School', salary: 2000, id: '2' },
  { title: 'bus driver', location: 'salta village', salary: 15000, id: '3' },
  { title: 'prison guard', location: 'alkatraz', salary: 5000, id: '4' },
  { title: 'manager', location: 'kfc', salary: 1500, id: '5' },
]);

const order = ref<OrderTerm>('title');

const handleClick = (term: OrderTerm) => {
  order.value = term;
};
</script>

<template>
  <div class="app">
    <header>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>

    <JobListComponent :jobs="jobs" :order="order" :handleClick="handleClick"/>
  </div>
</template>

<style scoped>
header {
  text-align: center;
}
header .order {
  margin-top: 20px;
}
button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
</style>
