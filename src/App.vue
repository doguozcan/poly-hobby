<script setup>
import { ref } from 'vue'
// hobbies array
const hobbies = ref([
  { category: 'Computer Science', activity: 'Code a webpage with vue.' },
  { category: 'Basketball', activity: 'Do a shooting training.' },
  { category: 'Movies', activity: 'Watch Rocky.' },
  { category: 'Basketball', activity: 'Watch an NBA game.' },
  { category: 'Computer Science', activity: 'Train competitive programming.' },
])
</script>

<template>
  <h1>Poly Hobby</h1>
  <ul>
    <li v-for="hobby in hobbies">
      {{ hobby.category }} - {{ hobby.activity }}
    </li>
  </ul>
</template>

<style></style>
