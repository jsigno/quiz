<script setup>
import { ref, computed } from 'vue';
const questions = ref([
  {
    question: 'What is Vue JS',
    answer: 0,
    options: [
      'A front end framework',
      'A library',
      'A ice cream maker'
    ],
    selected: null
  },
  {
    question: 'What is Vuex',
    answer: 2,
    options: [
      'The letter X after the word Vue',
      'A cheese stick',
      'State management library'
    ],
    selected: null
  },
  {
    question: 'What is Vue Router Used For?',
    answer: 1,
    options: [
      'An alternative route to route 64',
      'A routing library for Vue JS',
      'A drink from sonic'
    ],
    selected: null
  }
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const score = computed(() => {
  let value = 0
  questions.value.map(q => {
    if (q.selected == q.answer) {
      value++
    }
  })
  return value
})

</script>

<template>
<h1>
Hello World
</h1>
</template>

<style >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Monserrat', sans-serif;
}

body {
  background-color: #271c36;
  color: #fff;
}
</style>
