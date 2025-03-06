<template>
  <header class="flex items-center justify-between bg-green-100 py-4 px-6 shadow relative">
    <div class="flex items-center gap-4">
      <img src="~/assets/images/tima.jpg" class="w-14 h-14 rounded-full border-2 border-green-600 shadow-md" alt="Tima" />
      <span class="text-xl font-bold text-green-700 italic">Literally me</span>
    </div>

    <!-- Кнопка бургера -->
    <button @click="switch_burger" class="sm:hidden text-green-700 text-3xl">
      <span v-if="!burger">☰</span>
      <span v-else>✖</span>
    </button>

    <!-- Навбар -->
    <nav class="hidden sm:flex items-center gap-6">
      <NuxtLink to="/" class="nav-link">Home</NuxtLink>
      <div class="relative">
        <button class="nav-link" @click="switch_submenu">Labs</button>
        <div v-show="submenu" class="submenu">
          <NuxtLink v-for="lab in labs" :key="lab.path" :to="lab.path" class="submenu-item">
            {{ lab.name }}
          </NuxtLink>
        </div>
      </div>
      <NuxtLink to="/login" class="nav-link">LogIn</NuxtLink>
      <NuxtLink to="/logout" class="nav-link">LogOut</NuxtLink>
    </nav>

    <!-- Бургер на мобилках -->
    <div v-show="burger" class="absolute left-0 top-full w-full bg-green-50 flex flex-col items-center py-6 sm:hidden">
      <NuxtLink to="/" class="burger-link">Home</NuxtLink>
      <button class="burger-link" @click="switch_submenu">Labs</button>
      <div v-show="submenu" class="w-full flex flex-col">
        <NuxtLink v-for="lab in labs" :key="lab.path" :to="lab.path" class="burger-submenu">
          {{ lab.name }}
        </NuxtLink>
      </div>
      <NuxtLink to="/login" class="burger-link">LogIn</NuxtLink>
      <NuxtLink to="/logout" class="burger-link">LogOut</NuxtLink>
    </div>
  </header>

  <main class="p-5 bg-gray-50 min-h-screen">
    <slot />
  </main>

  <footer class="flex justify-center gap-4 bg-green-100 border-t px-4 py-3">
    <a v-for="icon in socialIcons" :key="icon.href" :href="icon.href" target="_blank">
      <img :src="icon.img" class="w-10 h-10 sm:w-16 sm:h-16 hover:scale-110 transition-transform" alt="Social Icon" />
    </a>
  </footer>
</template>

<script setup lang="ts">
import { useHead } from '#app';
import { ref } from 'vue';
import youtubeIcon from '~/assets/images/youtube.png';
import githubIcon from '~/assets/images/github.png';
import facebookIcon from '~/assets/images/facebook.png';

// Гугл таг
useHead({
  script: [
    {
      async: true,
      src: 'https://www.googletagmanager.com/gtag/js?id=G-XBXW09ZY7H',
    },
    {
      innerHTML: `
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', 'G-XBXW09ZY7H');
      `,
      type: 'text/javascript',
    },
  ],
  __dangerouslyDisableSanitizersByTagID: {
    gtag: ['innerHTML'],
  },
});

// Reactive Variables
const burger = ref(false);
const submenu = ref(false);

const switch_burger = () => {
  burger.value = !burger.value;
  if (!burger.value) submenu.value = false;
};

const switch_submenu = () => {
  submenu.value = !submenu.value;
};

const labs = [
  { name: 'Lab3', path: '/Lab3' },
  { name: 'Lab4', path: '/Lab4' },
  { name: 'Lab5', path: '/Lab5' },
  { name: 'Lab6', path: '/Lab6' }
];

const socialIcons = [
  { href: 'https://www.youtube.com/', img: youtubeIcon },
  { href: 'https://www.github.com/', img: githubIcon },
  { href: 'https://www.facebook.com/', img: facebookIcon }
];
</script>

<style scoped>
.nav-link {
  @apply p-2 text-green-700 hover:bg-green-200 hover:text-green-900 rounded-lg transition;
}

.submenu {
  @apply absolute top-full left-0 bg-green-50 text-green-700 w-40 text-center shadow-md sm:w-48 rounded-md;
}

.submenu-item {
  @apply block px-4 py-2 border-b border-green-200 hover:bg-green-300 hover:text-green-900;
}

.burger-link {
  @apply w-full text-center py-4 text-xl border-b border-green-200 hover:bg-green-300 hover:text-green-900;
}

.burger-submenu {
  @apply w-full text-center py-3 text-lg bg-green-200 border-b border-green-300 hover:bg-green-400 hover:text-green-900;
}
</style>