<script setup>
import { ref, computed, watch, onMounted } from 'vue'

// array where categories are stored
const categories = ['Science', 'Sport', 'Art']

// hobbies array
const hobbies = ref([
  { category: 'Science', activity: 'Make researchs on birds.' },
  { category: 'Sport', activity: 'Do a basketball shooting training.' },
  { category: 'Art', activity: 'Watch Rocky.' },
  { category: 'Sport', activity: 'Watch an NBA game.' },
  { category: 'Art', activity: 'Watch Twilight.' },
])

const reversedHobbies = computed(() => [...hobbies.value].reverse())

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

const name = ref('')

watch(name, (newName) => {
  localStorage.setItem('name', newName)
})

onMounted(() => {
  name.value = localStorage.getItem('name') || ''
})

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
