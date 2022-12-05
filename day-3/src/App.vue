<script setup>
import { watch, ref } from "vue";
import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "./components/CountdownSegment.vue";
import { useNow } from "@vueuse/core";

const now = useNow();
const christmas = new Date("12/25/2022 00:00:00");

const days = ref(null);
const hours = ref(null);
const minutes = ref(null);
const seconds = ref(null);

watch(now, (newVal) => {
  let difference = (christmas.getTime() - newVal.getTime()) / 1000;

  days.value = Math.floor(difference / 86400);
  difference -= days.value * 86400;

  hours.value = Math.floor(difference / 3600);
  difference -= hours.value * 3600;

  minutes.value = Math.floor(difference / 60);
  difference -= minutes.value * 60;

  seconds.value = Math.floor(difference);
});
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div
        class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]"
      >
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment
            label="days"
            :number="days"
          />
          <CountdownSegment
            label="hours"
            :number="hours"
          />
          <CountdownSegment
            label="minutes"
            :number="minutes"
          />
          <CountdownSegment
            label="seconds"
            :number="seconds"
          />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by
        <a
          href="https://vueschool.io/"
          class="underline"
        >
          Vue School
        </a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
