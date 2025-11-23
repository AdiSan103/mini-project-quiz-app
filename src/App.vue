<script setup lang="ts">
// type
interface TriviaResponse {
  response_code: number;
  results: TriviaQuestion[];
}

interface TriviaQuestion {
  type: string;
  difficulty: string;
  category: string;
  question: string;
  correct_answer: string;
  incorrect_answers: string[];
}

// import assets
import { ref } from "vue";
import Finish from "./component/Finish.vue";
import Loading from "./component/Loading.vue";
import Question from "./component/Question.vue";
import Start from "./component/Start.vue";
import axios from "axios";

// instance data
const isStart = ref<boolean>(true);
const isLoading = ref<boolean>(false);
const isQuestions = ref<boolean>(false);
const isFinish = ref<boolean>(false);
// list question
const listQuestions = ref<TriviaResponse>();
// list point answer
const listPoint = ref<number>(0);
// list queue question
const listQueue = ref<number>(0);

// methods
const clickStart = () => {
  isStart.value = false;
  isLoading.value = true;
  // ceritanya ada loading
  // setTimeout(() => {
  //   isLoading.value = false;
  //   isQuestions.value = true;
  // }, 3000);
  getData();
};

const getData = async () => {
  try {
    const response = await axios.get(
      "https://opentdb.com/api.php?amount=10&category=27&difficulty=easy&type=multiple"
    );
    listQuestions.value = response.data;
  } catch (error: any) {
    alert("error");
    console.log("error", error);
  } finally {
    isLoading.value = false;
    isQuestions.value = true;
  }
};

const updateQueue = () => {
  listQueue.value += 1;

  // end Finish
  if (listQueue.value === 10) {
    isFinish.value = true;
  }
};

const updatePoint = () => {
  listPoint.value += 1;
};

const resetQuiz = () => {
  isStart.value = true;
  isFinish.value = false;
  isLoading.value = false;
  isQuestions.value = false;
  listQuestions.value = {
    response_code: 0,
    results: [],
  };
  listPoint.value = 0;
  listQueue.value = 0;
};
</script>

<template>
  <Start v-if="isStart" @click-start="clickStart" />
  <Loading v-if="isLoading" />
  <div v-if="isQuestions" v-for="(item, index) in listQuestions?.results">
    <Question
      v-if="listQueue == index"
      :key="index"
      :type="item.type"
      :category="item.category"
      :difficulty="item.difficulty"
      :correct_answer="item.correct_answer"
      :question="item.question"
      :incorrect_answers="item.incorrect_answers"
      :now_question="listQueue + 1"
      :total_questions="listQuestions?.results?.length ?? 0"
      :now_point="listPoint"
      @update_queue="updateQueue"
      @update_point="updatePoint"
      @reset_quiz="resetQuiz"
    />
  </div>
  <Finish
    v-if="isFinish"
    :total_questions="10"
    :total_score="listPoint"
    @reset_quiz="resetQuiz()"
  />
</template>

<style lang="scss" scoped></style>
