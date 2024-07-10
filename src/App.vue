<script setup>
import { ref, computed, watch, onMounted } from 'vue'

// array where categories are stored
const categories = ['Science', 'Sport', 'Art']

// hobbies array
const hobbies = ref([])

// most recent added hobby is displayed first
const reversedHobbies = computed(() => [...hobbies.value].reverse())

// reactive and mutable ref object for the activity
const activity = ref('')

// reactive and mutable ref object for the category
const selectedCategory = ref('')

// function that adds hobby's category and activity type
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

// user's name
const name = ref('')

// save user's name to local storage
watch(name, (newName) => {
  localStorage.setItem('name', newName)
})

// save hobbies to local storage
watch(
  hobbies,
  (newHobbies) => {
    localStorage.setItem('hobbies', JSON.stringify(newHobbies))
  },
  { deep: true }
)

// when refresh, get values from local storage
onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  hobbies.value = JSON.parse(localStorage.getItem('hobbies') || '[]')
})

// seperate categories by colors
const categoryClass = (category) => {
  switch (category) {
    case 'Science':
      return 'category-science'
    case 'Sport':
      return 'category-sport'
    case 'Art':
      return 'category-art'
    default:
      return ''
  }
}
</script>

<template>
  <body>
    <h1>Poly Hobby</h1>
    <div class="greeting">
      <h2>Welcome</h2>
      <input placeholder="john doe" v-model="name" />
    </div>
    <input v-model="activity" placeholder="Enter your activity" />
    <select v-model="selectedCategory">
      <option v-for="category in categories">
        {{ category }}
      </option>
    </select>
    <button v-on:click="appendHobby">submit</button>
    <ul>
      <li
        v-for="hobby in reversedHobbies"
        :class="categoryClass(hobby.category)"
      >
        {{ hobby.category }} - {{ hobby.activity }}
      </li>
    </ul>
  </body>
</template>

<style></style>
