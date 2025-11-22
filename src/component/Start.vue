<script setup lang="ts">
import Button from "./Button.vue";
import Card from "./Card.vue";

const emit = defineEmits(["clickStart"]);
const doClickStart = () => {
  emit("clickStart");
};
</script>

<template>
  <Card class="start">
    <h1 class="start__title">Kuis Hewan</h1>
    <p class="start__desc">Uji pengetahuan Anda tentang dunia hewan!</p>
    <div class="start__contain">
      <p class="start__label">📝10 Pertanyaan</p>
      <p class="start__label">🎯Multiple Choice</p>
      <p class="start__label">⭐Tingkat: Mudah</p>
    </div>
    <Button variant="primary" title="Mulai" @click="doClickStart" />
  </Card>
</template>

<style lang="scss" scoped>
.start {
  &__title {
    color: #377ddc;
    font-size: 34.4;
  }

  &__desc {
    color: #6e818f;
    display: flex;
    margin: auto;
    margin-bottom: 30px;
    max-width: 200px;
  }

  &__label {
    color: #aeb3ac;
  }

  &__contain {
    margin-bottom: 20px;
  }
}
</style>
