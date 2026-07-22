<script setup>
import { ref } from 'vue'
import StartScreen from "./components/StartScreen.vue"
import QuestionScreen from "./components/QuestionScreen.vue"
import LoadingScreen from "./components/LoadingScreen.vue"
import ResultsScreen from "./components/ResultsScreen.vue"

const currentScreen = ref('start')
const quizResults = ref({})

const startQuiz = () => {
  currentScreen.value = 'question'
}

const handleQuizComplete = (ratings) => {
  quizResults.value = ratings
  currentScreen.value = 'loading'
}

const showResults = () => {
  currentScreen.value = 'results'
}

const restartQuiz = () => {
  quizResults.value = {}
  currentScreen.value = 'start'
}
</script>

<template>
  <StartScreen
    v-if="currentScreen === 'start'"
    @start-quiz="startQuiz"
  />

  <QuestionScreen
    v-if="currentScreen === 'question'"
    @quiz-complete="handleQuizComplete"
    @go-home="restartQuiz"
  />

  <LoadingScreen
    v-if="currentScreen === 'loading'"
    @loading-complete="showResults"
    @go-home="restartQuiz"
  />

  <ResultsScreen
    v-if="currentScreen === 'results'"
    :results="quizResults"
    @restart="restartQuiz"
    @go-home="restartQuiz"
  />
</template>
