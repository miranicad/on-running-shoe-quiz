<script setup>
import { ref } from 'vue'
import StartScreen from "./components/StartScreen.vue"
import QuestionScreen from "./components/QuestionScreen.vue"
import LoadingScreen from "./components/LoadingScreen.vue"
import ResultsScreen from "./components/ResultsScreen.vue"

const currentScreen = ref('start')
const quizResults = ref({})  // Speichert die Schuh-Ratings

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
  quizResults.value = {}  // Reset
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
  />

  <LoadingScreen
    v-if="currentScreen === 'loading'"
    @loading-complete="showResults"
  />

  <ResultsScreen
    v-if="currentScreen === 'results'"
    :results="quizResults"
    @restart="restartQuiz"
  />
</template>
