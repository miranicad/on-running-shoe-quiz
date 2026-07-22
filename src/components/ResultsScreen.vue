<script setup>
import { computed } from 'vue'
import NavBar from './NavBar.vue'
import quizData from '../../data.json'

const props = defineProps({
  results: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['restart', 'go-home'])


const sortedShoes = computed(() => {
  return quizData.shoes
    .map(shoe => ({
      ...shoe,
      rating: props.results[shoe.id] || 0
    }))
    .sort((a, b) => b.rating - a.rating)
})

const topShoe = computed(() => sortedShoes.value[0])

const similarShoes = computed(() => sortedShoes.value.slice(1, 3))

// Handles tie: returns all shoes with highest rating
const topShoes = computed(() => {
  const maxRating = sortedShoes.value[0]?.rating || 0
  return sortedShoes.value.filter(shoe => shoe.rating === maxRating)
})

const topShoesText = computed(() => {
  const names = topShoes.value.map(shoe => shoe.name)
  if (names.length === 1) {
    return names[0]
  } else if (names.length === 2) {
    return `${names[0]} and ${names[1]}`
  } else {
    return names.slice(0, -1).join(', ') + ' and ' + names[names.length - 1]
  }
})

const getShoeImage = (shoeName) => {
  return `${import.meta.env.BASE_URL}assets/${shoeName}.png`
}

const restartQuiz = () => {
  emit('restart')
}
</script>

<template>
  <div class="results-screen">
    <NavBar @go-home="emit('go-home')" />

    <main class="results-screen__content">
      <div class="results-screen__header">
        <h1>Congratulations!</h1>
        <p>Based on your selection we've decided on the {{ topShoesText }}! Enjoy the 30 day trial!</p>
      </div>

      <!-- Top Shoe Card -->
      <div class="results-screen__card">
        <div class="results-screen__image">
          <img :src="getShoeImage(topShoe.name)" :alt="topShoe.name" />
        </div>
        <h2>{{ topShoe.name }}</h2>
        <p class="results-screen__description">
          Your perfect partner in the world's lightest fully-cushioned shoe for Running Remixed.
        </p>
        <p class="results-screen__price">{{ topShoe.price }} CHF | {{ topShoe.color }}</p>
      </div>
      <button class="results-screen__shop-btn">Shop now</button>

      <!-- Similar Profiles -->
      <div class="results-screen__similar">
        <h3>Similar profiles</h3>

        <div class="results-screen__shoe-wrapper" v-for="shoe in similarShoes" :key="shoe.id">
          <div class="results-screen__card">
            <div class="results-screen__image">
              <img :src="getShoeImage(shoe.name)" :alt="shoe.name" />
            </div>
            <h2>{{ shoe.name }}</h2>
            <p class="results-screen__description">
              Your perfect partner in the world's lightest fully-cushioned shoe for Running Remixed.
            </p>
            <p class="results-screen__price">{{ shoe.price }} CHF | {{ shoe.color }}</p>
          </div>
          <button class="results-screen__shop-btn">Shop now</button>
        </div>
      </div>

      <!-- Restart Button -->
      <button class="results-screen__restart" @click="restartQuiz">
        Restart Quiz
      </button>
    </main>
  </div>
</template>

<style lang="scss" scoped>
@import '../style.scss';

.results-screen {
  min-height: 100vh;
  background-color: $white;
  display: flex;
  flex-direction: column;

  &__content {
    flex: 1;
    padding: 40px 20px;
    max-width: 500px;
    margin: 0 auto;
  }

  &__header {
    margin-bottom: 30px;

    h1 {
      font-size: 28px;
      font-weight: 400;
      margin-bottom: 10px;
    }

    p {
      font-size: 14px;
      color: $medium-gray;
      line-height: 1.5;
    }
  }

  &__shoe-wrapper {
    margin-bottom: 30px;
  }

  &__card {
    background-color: $card-bg;
    padding: 30px 20px;
    margin-bottom: 15px;

    h2 {
      font-size: 22px;
      font-weight: 400;
      color: $dark-text;
      margin-bottom: 10px;
    }
  }

  &__image {
    text-align: center;
    margin-bottom: 20px;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;

    img {
      width: 280px;
      height: 180px;
      object-fit: contain;
    }
  }

  &__description {
    font-size: 14px;
    color: $medium-gray;
    line-height: 1.5;
    margin-bottom: 15px;
  }

  &__price {
    font-size: 14px;
    color: $dark-text;
    font-weight: 500;
    margin-bottom: 20px;
  }

  &__shop-btn {
    display: block;
    width: 50%;
    margin: 0 auto;
    padding: 15px 30px;
    background-color: $primary-color;
    color: $white;
    border: none;
    cursor: pointer;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 2px;
    transition: background-color 0.3s ease;

    &:hover {
      background-color: $primary-color-hover;
    }
  }

  &__similar {
    margin-top: 40px;

    h3 {
      font-size: 22px;
      font-weight: 300;
      margin-bottom: 20px;
    }
  }

  &__restart {
    display: block;
    margin: 30px auto;
    padding: 10px 20px;
    background: none;
    border: none;
    color: $medium-gray;
    font-size: 14px;
    cursor: pointer;
    text-decoration: underline;

    &:hover {
      color: $dark-text;
    }
  }
}
</style>