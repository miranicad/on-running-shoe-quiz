<script setup>
import NavBar from './NavBar.vue'

const emit = defineEmits(['start-quiz'])

const backgroundImage = `${import.meta.env.BASE_URL}assets/Background Image Start Screen.png`

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
        <img :src="backgroundImage" alt="Runner" />
      </div>
    </main>
  </div>
</template>

<style lang="scss" scoped>
@import '../style.scss';

.start-screen {
  min-height: 100svh;
  background-color: $light-bg;
  display: flex;
  flex-direction: column;
  overflow: hidden;

  &__content {
    position: relative;
    flex: 1;
    min-height: 0;
    padding: 60px 40px;
    overflow: hidden;
    display: flex;
    align-items: center;

    &::after {
      content: '';
      position: absolute;
      right: 0;
      bottom: 0;
      left: 0;
      height: 350px;
      background: linear-gradient(
              to bottom,
              transparent,
              $light-bg
      );
      z-index: 3;
      pointer-events: none;
    }
  }

  &__text {
    position: relative;
    z-index: 2;
    max-width: 500px;
    animation: slideInLeft 1.2s ease-out forwards;
  }

  &__image {
    position: absolute;
    right: 0;
    bottom: -80px;
    height: 90%;
    z-index: 1;
    animation: slideInRight 1.2s ease-out forwards;

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
    color: $dark-text;
  }

  &__button {
    padding: 20px 50px;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 3px;
    background-color: $dark-bg;
    color: $white;
    border: 0;
    cursor: pointer;
    box-shadow: 4px 4px 0 rgba(0, 0, 0, 0.15);
    transition: transform 0.2s ease, box-shadow 0.2s ease;

    &:hover {
      transform: translate(-2px, -2px);
      box-shadow: 6px 6px 0 rgba(0, 0, 0, 0.15);
    }

    &:active {
      transform: translate(0, 0);
      box-shadow: 4px 4px 0 rgba(0, 0, 0, 0.15);
    }
  }

  &__subtitle {
    margin-top: 20px;
    font-size: 12px;
    color: $gray-text;
  }
}

@keyframes slideInRight {
  0% {
    transform: translateX(100%);
    opacity: 0;
  }
  20% {
    opacity: 1;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes slideInLeft {
  0% {
    transform: translateX(-100%);
    opacity: 0;
  }
  20% {
    opacity: 1;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}

@media (max-width: 1024px) and (min-width: 769px) {
  .start-screen {
    &__content {
      padding: 50px 30px;
      align-items: flex-start;

      &::after {
        height: 300px;
      }
    }

    &__text {
      max-width: 450px;
    }

    &__title {
      font-size: clamp(30px, 5vw, 42px);
      margin-bottom: 35px;
    }

    &__image {
      height: 85%;
      right: 0;

      img {
        height: 100%;
      }
    }
  }
}

@media (max-width: 768px) {
  .start-screen {
    &__content {
      padding: 90px 28px 20px;
      align-items: flex-start;

      &::after {
        height: 250px;
      }
    }

    &__text {
      width: 100%;
      max-width: 400px;
    }

    &__title {
      margin-bottom: 28px;
      font-size: clamp(28px, 8vw, 38px);
      line-height: 1.25;
    }

    &__image {
      right: -10%;
      top: auto;
      bottom: -10%;
      width: auto;
      height: 70%;

      img {
        display: block;
        width: auto;
        height: 100%;
      }
    }
  }
}
</style>