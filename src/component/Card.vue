<script setup lang="ts"></script>

<template>
  <div class="card">
    <div class="card__container">
      <slot />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.card {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  text-align: center;

  &__container {
    padding: 20px;
    border-radius: 13px;
    background: linear-gradient(135deg, hsl(240 25% 12%), hsl(240 20% 16%));
    width: 100%;
    max-width: 300px;
  }
}
</style>
