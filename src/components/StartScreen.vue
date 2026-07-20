<script setup>
import NavBar from './NavBar.vue'

const emit = defineEmits(['start-quiz'])

const startQuiz = () => {
  emit('start-quiz')
}
</script>

<template>
  <div class="start-screen">
    <NavBar />
    <main class="start-screen__content">
      <div class="start-screen__text">
        <h1 class="start-screen__title">
          Take the quiz<br>
          and try your first pair!
        </h1>

        <button class="start-screen__button" @click="startQuiz">
          Try On Trial
        </button>

        <p class="start-screen__subtitle">30 Days risk free</p>
      </div>

      <div class="start-screen__image">
        <img src="/assets/Background Image Start Screen.png" alt="Runner" />
      </div>
    </main>
  </div>
</template>

<style lang="scss" scoped>
.start-screen {
  min-height: 100vh;
  background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
}

.start-screen {
  &__content {
    flex: 1;
    display: flex;
    align-items: center;
    padding: 60px 40px;
    position: relative;
    overflow: hidden;
  }

  &__text {
    flex: 1;
    z-index: 2;
  }

  &__title {
    font-size: 48px;
    font-weight: 300;
    line-height: 1.2;
    color: #1a1a1a;
    margin-bottom: 40px;
  }

  &__button {
    display: inline-block;
    padding: 20px 50px;
    font-size: 16px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 3px;
    background-color: #1a1a1a;
    color: #ffffff;
    border: none;
    cursor: pointer;
    transition: all 0.3s ease;

    &:hover {
      background-color: #333333;
      transform: translateY(-2px);
    }
  }

  &__subtitle {
    margin-top: 20px;
    font-size: 14px;
    color: #888888;
  }

  &__image {
    position: absolute;
    right: 0;
    bottom: 0;
    width: 55%;
    height: 100%;

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      object-position: right bottom;
    }
  }
}

@media (max-width: 768px) {
  .start-screen {
    &__content {
      flex-direction: column;
      padding: 40px 20px;
    }

    &__title {
      font-size: 32px;
    }

    &__image {
      position: relative;
      width: 100%;
      height: auto;
      margin-top: 40px;
    }
  }
}
</style>