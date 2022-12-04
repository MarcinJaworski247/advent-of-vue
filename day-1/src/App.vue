<script setup>
import axios from "axios";
import LoadingSpinner from "./components/LoadingSpinner.vue";
import { ref, watch } from "vue";

const searchTerm = ref("");
const timeoutId = ref(null);
const resultList = ref([]);

const findProducts = async (term) => {
  if (term.trim().length === 0) {
    resultList.value = [];
    return;
  }

  axios
    .get(`https://dummyjson.com/products/search?q=${term}&limit=10`)
    .then((res) => {
      timeoutId.value = setTimeout(() => {
        console.log(term);
        resultList.value = res.data.products;
        timeoutId.value = null;
      }, 300);
    })
    .catch(() => {
      alert("Something went wrong!");
    });
};

watch(searchTerm, (newTerm) => findProducts(newTerm));
</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Gift Search Bar</h1>
    <input
      type="text"
      class="p-2 border-2 border-gray-dark"
      v-model="searchTerm"
      placeholder="Start typing..."
    />
    <loading-spinner v-if="timeoutId" />
    <template v-else>
      <ul>
        <li
          v-for="res in resultList"
          :key="res.id"
        >
          {{ res.title }} | {{ res.price }}$
        </li>
      </ul>
    </template>
  </div>
</template>
