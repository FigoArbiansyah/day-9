<template>
  <div
    class="p-4 bg-gradient-to-tr from-sky-500 to-sky-600 rounded-lg text-white text-center"
  >
    <h1 class="text-2xl font-semibold">Baca Al-Quran</h1>
    <p class="text-slate-100 mt-4 mb-2">
      Website Al-Quran dengan data yang lengkap
    </p>
    <!-- <p>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 mx-auto"
        fill="currentColor"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="1.5"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"
        ></path>
      </svg>
    </p> -->
  </div>
  <div class="mt-10 flex flex-wrap justify-center items-center bg-white">
    <div v-for="surah in surahs" class="w-full mb-3" :key="surah.number">
      <NuxtLink
        :to="`/surah/${surah.number}`"
        class="py-4 px-5 rounded hover:shadow-sm flex justify-between items-center hover:shadow-sky-500 transition-all ease duration-300 border border-white hover:border-sky-500 hover:-translate-y-1"
      >
        <div class="flex items-center gap-x-3">
          <div class="relative h-11 w-11 flex items-center justify-center">
            <span class="text-slate-700">{{ surah.number }}</span>
            <svg
              class="absolute"
              viewBox="0 0 46 46"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M23 1.46451L28.8707 7.7459L29.181 8.07785L29.6351 8.06251L38.2279 7.77211L37.9375 16.3649L37.9221 16.819L38.2541 17.1293L44.5355 23L38.2541 28.8707L37.9221 29.181L37.9375 29.6351L38.2279 38.2279L29.6351 37.9375L29.181 37.9221L28.8707 38.2541L23 44.5355L17.1293 38.2541L16.819 37.9221L16.3649 37.9375L7.77211 38.2279L8.06251 29.6351L8.07785 29.181L7.7459 28.8707L1.46451 23L7.7459 17.1293L8.07785 16.819L8.06251 16.3649L7.77211 7.77211L16.3649 8.06251L16.819 8.07785L17.1293 7.7459L23 1.46451Z"
                stroke="rgb(14 165 233)"
                stroke-width="1"
              ></path>
            </svg>
          </div>
          <div>
            <p class="text-xl font-semibold">
              {{ surah?.name?.transliteration?.id }}
            </p>
            <p class="text-slate-700">{{ surah?.name?.translation?.id }}</p>
          </div>
        </div>
        <div>
          <p class="text-2xl font-semibold ayah surah">{{ surah.name?.short }}</p>
        </div>
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
const url = "https://api.quran.gading.dev/surah";
async function getSurahs() {
  const response = await axios.get(url);
  return response.data.data;
}
const surahs = await getSurahs();
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Scheherazade+New:wght@400;700&display=swap");
.surah {
  font-family: "Scheherazade New", serif;
}
</style>
