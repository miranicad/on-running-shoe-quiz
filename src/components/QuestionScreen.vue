<script setup>
import { ref, computed } from 'vue'
import NavBar from './NavBar.vue'
import quizData from '../../data.json'

const emit = defineEmits(['quiz-complete', 'go-home'])

const currentQuestionId = ref(0)
const shoeRatings = ref({})

quizData.shoes.forEach(shoe => {
  shoeRatings.value[shoe.id] = 0
})

const currentQuestion = computed(() => {
  return quizData.questions.find(q => q.id === currentQuestionId.value)
})

const selectAnswer = (answer) => {
  for (const [shoeId, points] of Object.entries(answer.ratingIncrease)) {
    shoeRatings.value[shoeId] += points
  }

  if (answer.nextQuestion === '') {
    emit('quiz-complete', shoeRatings.value)
  } else {
    currentQuestionId.value = answer.nextQuestion
  }
}
</script>

<template>
  <div class="question-screen">
    <NavBar @go-home="emit('go-home')" />

    <main class="question-screen__content">
      <div class="question-screen__header">
        <p class="question-screen__subtitle">TRY ON QUIZ</p>
        <p class="question-screen__subtitle">30 DAYS RISK FREE</p>
      </div>

      <h2 class="question-screen__question">
        {{ currentQuestion.copy }}
      </h2>

      <div class="question-screen__answers">
        <button
          v-for="answer in currentQuestion.answers"
          :key="answer.copy"
          class="question-screen__answer"
          @click="selectAnswer(answer)"
        >
          {{ answer.copy }}
        </button>
      </div>
    </main>
  </div>
</template>

<style lang="scss" scoped>
@import '../style.scss';

.question-screen {
  min-height: 100vh;
  background-color: $question-bg;
  display: flex;
  flex-direction: column;
  touch-action: manipulation;

  &__content {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 40px;
    color: $white;
  }

  &__header {
    text-align: center;
    margin-bottom: 80px;
  }

  &__subtitle {
    font-size: 12px;
    letter-spacing: 6px;
    color: $light-gray;
  }

  &__question {
    font-size: 42px;
    font-weight: 300;
    text-align: center;
    flex: 1;
    display: flex;
    align-items: center;
    max-width: 600px;
  }

  &__answers {
    display: flex;
    gap: 20px;
    width: 100%;
    max-width: 700px;
    margin-bottom: 200px;
  }

  &__answer {
    flex: 1;
    padding: 25px 40px;
    font-size: 18px;
    background-color: transparent;
    color: $white;
    border: 1px solid $white;
    cursor: pointer;
    transition: all 0.3s ease;

    &:hover {
      background-color: $white;
      color: $question-bg;
    }
  }
}

@media (max-width: 768px) {
  .question-screen {
    &__question {
      font-size: 28px;
    }

    &__answer {
      padding: 20px;
      font-size: 14px;
      white-space: nowrap;
    }
  }
}
</style>