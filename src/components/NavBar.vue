<script setup>
import { ref } from 'vue'

defineProps(['isDark'])
const emit = defineEmits(['toggle-dark'])

const menuOpen = ref(false)
const links = ['About', 'Projects', 'Skills', 'Contact']
</script>

<template>
  <nav class="fixed top-0 w-full z-50 bg-stone-50/80 dark:bg-zinc-950/80 backdrop-blur-md border-b border-stone-200 dark:border-zinc-800">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <!-- Logo -->
        <a href="#" class="font-display text-xl font-bold text-zinc-900 dark:text-stone-100">
          Radit Shalom<span class="text-amber-500">.</span>
        </a>

        <!-- Desktop Links -->
        <div class="hidden md:flex items-center gap-8">
          
          <a  v-for="link in links"
            :key="link"
            :href="`#${link.toLowerCase()}`"
            class="text-sm text-zinc-600 dark:text-zinc-400 hover:text-zinc-900 dark:hover:text-stone-100 transition-colors"
          >{{ link }}</a>
        </div>

        <!-- Dark Mode + Mobile Menu -->
        <div class="flex items-center gap-3">
          <!-- Dark Toggle -->
          <button @click="$emit('toggle-dark')" class="p-2 rounded-lg hover:bg-stone-200 dark:hover:bg-zinc-800 transition-colors">
            <span v-if="isDark" class="text-lg">☀️</span>
            <span v-else class="text-lg">🌙</span>
          </button>

          <!-- Mobile Hamburger -->
          <button @click="menuOpen = !menuOpen" class="md:hidden p-2 rounded-lg hover:bg-stone-200 dark:hover:bg-zinc-800">
            <div class="w-5 h-0.5 bg-zinc-900 dark:bg-stone-100 mb-1 transition-all" :class="{'rotate-45 translate-y-1.5': menuOpen}"></div>
            <div class="w-5 h-0.5 bg-zinc-900 dark:bg-stone-100 mb-1 transition-all" :class="{'opacity-0': menuOpen}"></div>
            <div class="w-5 h-0.5 bg-zinc-900 dark:bg-stone-100 transition-all" :class="{'-rotate-45 -translate-y-1.5': menuOpen}"></div>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div v-show="menuOpen" class="md:hidden pb-4 flex flex-col gap-3">

        <a  v-for="link in links"
          :key="link"
          :href="`#${link.toLowerCase()}`"
          @click="menuOpen = false"
          class="text-zinc-700 dark:text-zinc-300 py-1 hover:text-amber-500 transition-colors"
        >{{ link }}</a>
      </div>
    </div>
  </nav>
</template>