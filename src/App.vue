<script setup>
import { ref, computed } from 'vue'
// hobbies array
const hobbies = ref([
  { category: 'Computer Science', activity: 'Code a webpage with vue.' },
  { category: 'Basketball', activity: 'Do a shooting training.' },
  { category: 'Movies', activity: 'Watch Rocky.' },
  { category: 'Basketball', activity: 'Watch an NBA game.' },
  { category: 'Computer Science', activity: 'Train competitive programming.' },
])

const reversedHobbies = computed(() => [...hobbies.value].reverse())

// array where categories are stored
const categories = ['Computer Science', 'Basketball', 'Movies']

// reactive and mutable ref object for the activity
const activity = ref('')

// reactive and mutable ref object for the category
const selectedCategory = ref('')

const appendHobby = () => {
  if (activity.value && selectedCategory.value) {
    hobbies.value.push({
      category: selectedCategory.value,
      activity: activity.value,
    })

    selectedCategory.value = ''
    activity.value = ''
  } else {
    alert('Please enter both activity and category values.')
  }
}
</script>

<template>
  <h1>Poly Hobby</h1>
  <input v-model="activity" placeholder="Enter your activity" />
  <select v-model="selectedCategory">
    <option v-for="category in categories">
      {{ category }}
    </option>
  </select>
  <button v-on:click="appendHobby">submit</button>
  <li v-for="hobby in reversedHobbies">
    {{ hobby.category }} - {{ hobby.activity }}
  </li>
</template>

<style></style>
