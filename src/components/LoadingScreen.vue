<script setup>
import { onMounted } from 'vue'
import NavBar from './NavBar.vue'

const emit = defineEmits(['loading-complete'])

onMounted(() => {
  setTimeout(() => {
    emit('loading-complete')
  }, 2000)
})
</script>

<template>
  <div class="loading-screen">
    <NavBar />

    <main class="loading-screen__content">
      <img src="/assets/loader.gif" alt="Loading..." class="loading-screen__loader" />
      <p class="loading-screen__text">We're running to get your results.</p>
    </main>
  </div>
</template>

<style lang="scss" scoped>
.loading-screen {
  min-height: 100vh;
  background-color: #333333;
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
    color: #666666;
    font-size: 18px;
    letter-spacing: 2px;
  }
}
</style>