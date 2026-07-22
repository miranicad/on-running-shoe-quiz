<script setup>
import { onMounted } from 'vue'
import NavBar from './NavBar.vue'

const emit = defineEmits(['loading-complete', 'go-home'])

const loaderImage = `${import.meta.env.BASE_URL}assets/loader.gif`

onMounted(() => {
  setTimeout(() => {
    emit('loading-complete')
  }, 2000)
})
</script>

<template>
  <div class="loading-screen">
    <NavBar @go-home="emit('go-home')" />

    <main class="loading-screen__content">
      <img :src="loaderImage" alt="Loading..." class="loading-screen__loader" />
      <p class="loading-screen__text">We're running to get your results.</p>
    </main>
  </div>
</template>

<style lang="scss" scoped>
@import '../style.scss';

.loading-screen {
  min-height: 100vh;
  background-color: $question-bg;
  display: flex;
  flex-direction: column;

  &__content {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 40px;
  }

  &__loader {
    width: 80px;
    height: 80px;
    margin-bottom: 30px;
  }

  &__text {
    color: $medium-gray;
    font-size: 18px;
    letter-spacing: 2px;
    text-align: center;
    white-space: nowrap;
  }
}
</style>