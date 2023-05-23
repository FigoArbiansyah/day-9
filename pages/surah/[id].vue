<template>
  <div
    class="p-4 bg-gradient-to-tr from-sky-500 to-sky-600 rounded-lg text-white text-center relative"
  >
    <h1 class="text-2xl font-semibold">{{surah.name?.transliteration?.id}}</h1>
    <p class="text-slate-100 mt-1 mb-2">
      {{surah.name?.translation?.id}}
    </p>
    <hr class="md:w-1/3 mx-auto w-9/12 mt-3 mb-2">
    <p class="text-slate-50">
      <span>{{surah?.revelation?.id}} - </span>
      <span> {{`${surah?.numberOfVerses}  Ayat`}}</span>
    </p>
    <div class="hidden text-justify text-slate-100" id="detailSurah">
      <p>Tafsir: </p>
      <p>{{surah?.tafsir?.id}}</p>
    </div>
    <div class="absolute top-3 left-3 cursor-pointer" @click="showDetailSurah()">
      📖
    </div>
  </div>
  <div class="mt-4 mb-8">
    <div v-if="surah.name?.transliteration?.id != 'Al-Fatihah'" class="flex justify-center pt-3">
      <img src="~/assets/img/bismillah.svg" class="scale-75">
    </div>
    <div v-for="verse in surah.verses" class="mt-10 flex justify-between items-start pb-6 border-b">
      <div class="w-2/12 flex flex-col gap-y-5 items-start">
        <div class="relative h-11 w-11 flex items-center justify-center">
          <span class="text-slate-700 text-sm">{{ verse?.number?.inSurah }}</span>
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
        <div class="ml-[0.68rem] cursor-pointer group" @click="showDetail(verse?.number?.inQuran)">
          <button>📘</button>
        </div>
        <!-- <div class="ml-[0.55rem] cursor-pointer group" @click="mark(verse?.number?.inQuran)">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 mx-auto bookmark"
            :fill="checkAyah(verse)"
            viewBox="0 0 24 24"
            stroke="rgb(14 165 233)"
            stroke-width="1"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"
            ></path>
          </svg>
        </div> -->
      </div>
      <div class="ayah text-end w-10/12">
        <p class="text-3xl surah text-gray-900 leading-[4rem]">{{verse?.text?.arab}}</p>
        <p class="text-slate-600 mt-3">{{verse?.text?.transliteration?.en}}</p>
        <p class="text-slate-500 mt-3">{{verse?.translation?.id}}</p>
        <div class="hidden mt-5 text-start -ml-[4rem]" :id="verse?.number?.inQuran">
          <p class="text-slate-500">Tafsir:</p>
          <p class="text-slate-500">{{verse?.tafsir?.id?.short}}</p>
        </div>
      </div>
    </div>
    <!-- <div class="flex gap-x-10 mx-auto justify-center pt-5">
      <NuxtLink class="hover:text-sky-600" :to="`/surah/${surah.number - 1 == 0 ? '1' : surah.number -= 1}`">Sebelumnya</NuxtLink>
      <NuxtLink class="hover:text-sky-600" :to="`/surah/${surah.number + 1 == 1 ? '114' : surah.number += 1}`">Selanjutnya</NuxtLink>
    </div> -->
  </div>
</template>

<script setup>
import axios from "axios";
function showDetail(id) {
  const tafsir = document.getElementById(id)
  tafsir.classList.toggle("hidden")
}

function showDetailSurah() {
  const detailSurah = document.getElementById("detailSurah")
  detailSurah.classList.toggle("hidden")
}

const route = useRoute();
const id = route.params.id;

const url = "https://api.quran.gading.dev/surah/" + id;
async function getSurah() {
  const response = await axios.get(url);
  return response.data.data;
}
const surah = await getSurah();








// function checkAyah(ayat) {
//   const mark = JSON.parse(localStorage.getItem("mark")) || []
//   return mark.includes(ayat?.number?.inQuran) ? "rgb(14 165 233)" : "none"
// }

// function mark(number) {
//   const mark = JSON.parse(localStorage.getItem("mark")) || []
//   const filter = mark.filter(m => {
//     return m.number == number
//   })
//   if (filter.length > 0) {
//     alert("Ayat ini sudah ditandai!")
//     return;
//   }
//   const data = number
//   mark.push(data)
//   localStorage.setItem("mark", JSON.stringify(mark))
// }

</script>
