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

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})

const SetAnswer = event => {
  questions.value[currentQuestion.value].selected = event.target.value
  event.target.value = null
}

const NextQuestion = () => {
  if (currentQuestion.value < questions.value.length -1) {
    currentQuestion.value++
  } else {
    quizCompleted.value = true
  }
}

</script>

<template>
	<main class="app">
		<h1>The Quiz</h1>
		
		<section class="quiz" v-if="!quizCompleted">
			<div class="quiz-info">
				<span class="question">{{ getCurrentQuestion.question }}</span>
				<span class="score">Score {{ score }}/{{ questions.length }}</span>
			</div>
			
			<div class="options">
				<label 
					v-for="(option, index) in getCurrentQuestion.options" 
					:for="'option' + index" 
					:class="`option ${
						getCurrentQuestion.selected == index 
							? index == getCurrentQuestion.answer 
								? 'correct' 
								: 'wrong'
							: ''
					} ${
						getCurrentQuestion.selected != null &&
						index != getCurrentQuestion.selected
							? 'disabled'
							: ''
					}`">
					<input 
						type="radio" 
						:id="'option' + index" 
						:name="getCurrentQuestion.index" 
						:value="index" 
						v-model="getCurrentQuestion.selected" 
						:disabled="getCurrentQuestion.selected"
						@change="SetAnswer" 
					/>
					<span>{{ option }}</span>
				</label>
			</div>
			
			<button 
				@click="NextQuestion" 
				:disabled="!getCurrentQuestion.selected">
				{{ 
					getCurrentQuestion.index == questions.length - 1 
						? 'Finish' 
						: getCurrentQuestion.selected == null
							? 'Select an option'
							: 'Next question'
				}}
			</button>
		</section>

		<section v-else>
			<h2>You have finished the quiz!</h2>
			<p>Your score is {{ score }}/{{ questions.length }}</p>
		</section>
	</main>
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
