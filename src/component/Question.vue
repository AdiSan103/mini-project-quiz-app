<script setup lang="ts">
// type
interface TriviaQuestion {
  type: string;
  difficulty: string;
  category: string;
  question: string;
  correct_answer: string;
  incorrect_answers: string[];
  total_questions: number;
  now_question: number;
  now_point: number;
}

import { ref } from "vue";
// assets
import Button from "./Button.vue";
import Card from "./Card.vue";

// instance vue
const emit = defineEmits(["update_queue", "update_point", "reset_quiz"]);
const props = defineProps<TriviaQuestion>();
const selectedAnswer = ref<string | null>(null);
const isAnswered = ref(false); // user sudah menjawab atau belum
// ==== questions ====
// 3️⃣ .sort(() => Math.random() - 0.5)
// Ini adalah trik umum untuk mengacak urutan array.
// Cara kerjanya:
// Math.random() → menghasilkan angka acak dari 0–1
// Math.random() - 0.5 → menghasilkan angka dari -0.5 sampai 0.5
// .sort() akan mengurutkan berdasarkan angka acak tersebut → hasilnya acak.
// Contoh:
// Jika hasil random negatif → elemen ditukar.
// Jika hasil random positif → elemen tetap.
const listQuestion = [...props.incorrect_answers, props.correct_answer].sort(
  () => Math.random() - 0.5
);

// method
const checkAnswer = (answer: string) => {
  if (isAnswered.value) {
    // alert("anda sudah menjawab, lanjut berikutnya!");
    return;
  } // cegah user klik lagi

  selectedAnswer.value = answer;
  isAnswered.value = true;

  if (answer === props.correct_answer) {
    emit("update_point");
  }
};

const getVariant = (item: string) => {
  if (!selectedAnswer.value) return "default"; // default sebelum memilih

  // Jika jawaban benar
  if (item === props.correct_answer) return "success";

  // Jika jawaban salah & dipilih user
  if (item === selectedAnswer.value) return "danger";

  // Jawaban salah tapi tidak dipilih user
  return "default";
};

const nextQuestion = () => {
  emit("update_queue");
};

const resetQuiz = () => {
  emit("reset_quiz");
};
</script>

<template>
  <Transition>
    <Card class="question">
      <!-- navbar -->
      <div class="question__navbar">
        <p class="question__title">
          Pertanyaan {{ now_question }} dari {{ total_questions }}
        </p>
        <p class="question__score">Skor: {{ now_point }}</p>
        <div class="question__icon-back" @click="resetQuiz">
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M5 17V15C5 10.0294 8.80558 6 13.5 6C18.1944 6 22 10.0294 22 15"
              stroke="white"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              d="M8 15L5 18L2 15"
              stroke="white"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </div>
      </div>
      <!-- bar -->
      <div class="question__bar"></div>
      <!-- question -->
      <p class="question__quiz">
        {{ question }}
      </p>
      <!-- answer option -->
      <!-- @submit.prevent = Menangkap event submit pada form dan mencegah perilaku default-nya, yaitu mencegah halaman reload. -->
      <div class="question__options">
        <Button
          v-for="item in listQuestion"
          :key="item"
          :title="item"
          :variant="getVariant(item)"
          @click="checkAnswer(item)"
        />
      </div>
      <Button
        v-if="isAnswered"
        title="Next Question"
        variant="primary"
        @click="nextQuestion()"
      />
    </Card>
  </Transition>
</template>

<style lang="scss" scoped>
.question {
  &__icon-back {
    cursor: pointer;
    border: 1px solid #4a4a4a;
    height: 30px;
    width: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
  }
  &__navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  &__title {
    color: #0a88c0;
  }
  &__score {
    color: #50349b;
  }

  &__bar {
    background: linear-gradient(135deg, hsl(260 60% 55%), hsl(195 100% 50%));
    width: 100%;
    height: 20px;
    border-radius: 100px;
    margin-top: 10px;
    margin-bottom: 10px;
  }

  &__quiz {
    color: #b6bcbe;
    margin-top: 20px;
    margin-bottom: 20px;
  }

  &__options {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin-bottom: 40px;
  }
}
</style>
