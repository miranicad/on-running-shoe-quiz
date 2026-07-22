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
  min-height: 100svh;
  background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
  overflow: hidden;

  &__content {
    position: relative;
    flex: 1;
    min-height: 0;
    padding: 60px 40px;
    overflow: hidden;

    &::after {
      content: '';
      position: absolute;
      right: 0;
      bottom: 0;
      left: 0;
      height: 220px;
      background: linear-gradient(
              to bottom,
              transparent,
              #f5f5f5
      );
      z-index: 3;
      pointer-events: none;
    }
  }

  &__text {
    position: relative;
    z-index: 2;
    max-width: 400px;
  }

  &__image {
    position: absolute;
    right: 0;
    bottom: 0;
    height: 85%;
    z-index: 1;

    img {
      display: block;
      width: auto;
      height: 100%;
      max-width: none;
      object-fit: contain;
      object-position: right bottom;
    }
  }

  &__title {
    margin: 0 0 40px;
    font-size: clamp(32px, 4vw, 48px);
    font-weight: 300;
    line-height: 1.4;
    color: #1a1a1a;
  }

  &__button {
    padding: 20px 50px;
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 3px;
    background-color: #1a1a1a;
    color: #ffffff;
    border: 0;
    cursor: pointer;
  }

  &__subtitle {
    margin-top: 20px;
    font-size: 12px;
    color: #888888;
  }
}

@media (max-width: 768px) {
  .start-screen {
    &__content {
      padding: 90px 28px 20px;

      &::after {
        height: 120px;
      }
    }

    &__text {
      width: 100%;
    }

    &__title {
      margin-bottom: 28px;
      font-size: clamp(28px, 8vw, 38px);
      line-height: 1.25;
    }

    &__image {
      right: -22%;
      bottom: 80px;
      width: 125%;
      height: auto;

      img {
        display: block;
        width: 100%;
        height: auto;
      }
    }
  }
}
</style>