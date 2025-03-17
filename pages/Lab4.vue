<script setup lang="ts">
import { reactive, ref } from "vue";

// Реактив аррей для аудишек
const audios = reactive([
  { name: "In the Beginning", src: "/audio/In the beginning.mp3" },
  { name: "The Binding of Isaac", src: "/audio/The Binding of Isaac.mp3" },
  { name: "Greed", src: "/audio/Greed.mp3" }
]);

// Реактив реф, чтобы хранить выбранные треки
const selectedAudio = ref("");
</script>

<template>
  <main class="flex flex-col items-center min-h-screen bg-gradient-to-br from-gray-200 to-blue-100 p-10">
    <h1 class="text-4xl font-bold mb-6 text-gray-900">🎵 Some cool soundtracks from the game</h1>

    <!-- Красивые аудио карточки -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 w-full max-w-4xl">
      <div
        v-for="audio in audios"
        :key="audio.name"
        class="bg-white p-6 rounded-lg shadow-lg border hover:shadow-xl transition transform hover:scale-105 flex flex-col items-center gap-3"
      >
        <!-- Названия аудио -->
        <p class="text-lg font-semibold text-gray-800">{{ audio.name }}</p>

        <!-- Кастомная кнопочка нажатия -->
        <button
          @click="selectedAudio = audio.src"
          class="px-4 py-2 bg-blue-500 text-white font-semibold rounded-full shadow-md hover:bg-blue-600 transition"
        >
          ▶ Play
        </button>
      </div>
    </div>

    <!-- Аудио плеер -->
    <div v-if="selectedAudio" class="mt-8 p-4 bg-white rounded-lg shadow-lg border w-full max-w-lg">
      <audio :src="selectedAudio" controls class="w-full"></audio>
    </div>
  </main>
</template>