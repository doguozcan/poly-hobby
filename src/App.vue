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

// array where categories are stored
const categories = ['Computer Science', 'Basketball', 'Movies']

// reactive and mutable ref object for the activity
const activity = ref('')

// reactive and mutable ref object for the category
const selectedCategory = ref('')
</script>

<template>
  <h1>Poly Hobby</h1>
  <input v-model="activity" placeholder="Enter your activity" />
  <select v-model="selectedCategory">
    <option v-for="category in categories">
      {{ category }}
    </option>
  </select>
  <li v-for="hobby in hobbies">{{ hobby.category }} - {{ hobby.activity }}</li>
</template>

<style></style>
