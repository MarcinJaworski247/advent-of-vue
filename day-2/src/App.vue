<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="w-1/2">
      <div class="flex justify-start">
        <div class="w-1/2 mb-2 joke joke--question">
          {{ question }}
        </div>
      </div>

      <div
        v-if="isAnswerShown"
        class="flex justify-end"
      >
        <div class="w-1/2 mb-2 joke joke--answer">
          {{ answer }}
        </div>
      </div>

      <button
        type="button"
        class="btn"
        v-if="!isAnswerShown"
        @click="showAnswer"
      >
        Tell me!
      </button>
      <button
        type="button"
        class="btn"
        v-if="isAnswerShown"
        @click="fetchNextJoke"
      >
        Another one
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const question = ref("");
const answer = ref("");
const isAnswerShown = ref(false);

const fetchJoke = () => {
  axios
    .get("https://v2.jokeapi.dev/joke/christmas")
    .then((res) => {
      question.value = res.data.setup;
      answer.value = res.data.delivery;
    })
    .catch(() => {
      alert("Something went wrong!");
    });
};

onMounted(() => {
  fetchJoke();
});

const showAnswer = () => {
  isAnswerShown.value = true;
};

const fetchNextJoke = () => {
  fetchJoke();
  isAnswerShown.value = false;
};
</script>

<style lang="scss" scoped>
.btn {
  background-color: #42b883;
  color: #fff;
  border-radius: 7px;
  width: 100%;
  display: block;
  padding-top: 8px;
  padding-bottom: 8px;

  &:hover {
    opacity: 0.9;
  }
}
.joke {
  color: #fff;
  padding: 16px 32px;
  border-radius: 7px;
  transition: 0.3s ease;

  &--question {
    background-color: #115e59;
  }

  &--answer {
    background-color: #991b1b;
  }
}
</style>
