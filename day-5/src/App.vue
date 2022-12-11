<template>
  <div class="w-full h-full flex justify-center items-center">
    <div>
      <div class="w-full max-w-2xl p-4 rounded bg-red-400 text-white">
        <div
          class="border-2 rounded flex flex-col md:flex-row md:items-center md:gap-8 p-4"
        >
          <img
            src="/santa.svg"
            alt=""
            class="max-w-[12em]"
          />
          <div>
            <h1 class="font-serif text-4xl">Happy Holidays!</h1>
            <div class="mt-4 bg-white text-black p-2 rounded">TO: {{ to }}</div>
            <div class="mt-2 bg-white text-black p-2 rounded">
              FROM: {{ from }}
            </div>
          </div>
        </div>
      </div>
      <div class="mt-4">
        <label
          for="to"
          class="block"
        >
          To
        </label>
        <input
          type="text"
          id="to"
          v-model="to"
          class="w-full bg-gray-50 border border-gray-300 rounded-lg p-2"
        />
        <label
          for="from"
          class="block mt-2"
        >
          From
        </label>
        <input
          type="text"
          id="from"
          v-model="from"
          class="w-full bg-gray-50 border border-gray-300 rounded-lg p-2"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const to = ref("");
const from = ref("");
</script>
