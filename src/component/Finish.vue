<script setup lang="ts">
import Button from "./Button.vue";
import Card from "./Card.vue";

interface Props {
  total_score: number;
  total_questions: number;
}

defineProps<Props>();
const emit = defineEmits(["reset_quiz"]);
const resetQuiz = () => {
  emit("reset_quiz");
};
</script>

<template>
  <Card class="finish">
    <h2 class="finish__title">Kuis Selesai! 🥳</h2>
    <p class="finish__desc">Terima kasih telah mengikuti kuis ini</p>
    <div class="finish__score">
      <h3 class="finish__scoretitle">Skor Akhir Anda:</h3>
      <p class="finish__scoredesc">{{ total_score }}/{{ total_questions }}</p>
    </div>
    <p class="finish__text">Tetap semangat! Mari coba lagi! 💪</p>
    <Button title="Main Lagi" variant="primary" @click="resetQuiz()" />
  </Card>
</template>

<style lang="scss" scoped>
.finish {
  &__title {
    color: #d2d6d9;
  }
  &__desc {
    color: #5f6f7d;
  }
  &__score {
    background: linear-gradient(135deg, hsl(260 60% 55%), hsl(195 100% 50%));
    padding: 20px;
    border-radius: 10px;
    margin-top: 20px;
    margin-bottom: 20px;
  }
  &__scoredesc {
    font-size: 58px;
  }
  &__text {
    color: #8e9496;
    margin-top: 10px;
    margin-bottom: 40px;
  }
}
</style>
