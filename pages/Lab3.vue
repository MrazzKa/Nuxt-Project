<script setup lang="ts">
import { ref } from 'vue';

// Реактив, чтобы контролировать видимость видоса
const showVideo = ref(false);
</script>

<template>
  <main class="flex flex-col items-center p-10 bg-gray-100">
    <h1 class="text-3xl font-bold mb-4">This is "The Binding of Isaac" Trailer</h1>

    <!-- Кнопочка чтобы показать/скрыть видео -->
    <button 
      @click="showVideo = !showVideo" 
      class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-700 transition"
    >
      {{ showVideo ? 'Hide Video' : 'Show Video' }}
    </button>

    <!-- Видео плеер (Появляется только когда кликаешь) -->
    <video v-show="showVideo" controls class="w-96 mt-4 border-2 border-blue-500 rounded-lg">
      <source src="~/assets/images/Isaac Trailer.mp4" type="video/mp4">
      Your browser does not support the video tag.
    </video>
  </main>
</template>
