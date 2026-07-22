<script setup>
</script>

<template>
  <nav class="navbar">
    <button class="navbar__menu" aria-label="Menu">
      <span class="navbar__menu-line"></span>
      <span class="navbar__menu-line"></span>
      <span class="navbar__menu-line"></span>
    </button>
    <div class="navbar__logo">
     <img src="/assets/On-Logo.png">
    </div>
  </nav>
</template>

<style lang="scss" scoped>
.navbar {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px 40px;
  background-color: #ffffff;
  position: relative;

  &__menu {
    position: absolute;
    left: 40px;
    display: flex;
    flex-direction: column;
    gap: 5px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 5px;

    &-line {
      display: block;
      width: 24px;
      height: 2px;
      background-color: #1a1a1a;
      transition: background-color 0.3s ease;
    }

    &:hover .navbar__menu-line {
      background-color: #00a6a6;
    }
  }

  &__logo {
    img {
      height: 40px;
      width: auto;
      display: block;
    }
  }
}

@media (max-width: 768px) {
  .navbar {
    padding: 15px 20px;

    &__menu {
      left: 20px;
    }
  }
}
</style>