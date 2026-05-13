<script setup>
import { onMounted, onUnmounted, ref , computed } from 'vue'

const props = defineProps(['project'])
const emit = defineEmits(['close'])

const lightboxImg = ref(null)

const filteredImages = computed(() =>
  (props.project.images || []).filter(img => img)
)
const openLightbox = (img) => { lightboxImg.value = img }
const closeLightbox = () => { lightboxImg.value = null }

const handleKey = (e) => {
  if (e.key === 'Escape') {
    if (lightboxImg.value) closeLightbox()
    else emit('close')
  }
}

onMounted(() => {
  document.addEventListener('keydown', handleKey)
  document.body.style.overflow = 'hidden'
})
onUnmounted(() => {
  document.removeEventListener('keydown', handleKey)
  document.body.style.overflow = ''
})
</script>

<template>
  <Teleport to="body">

    <!-- ─── Lightbox ─── -->
    <Transition name="fade">
      <div
        v-if="lightboxImg"
        class="fixed inset-0 z-[60] bg-black/90 flex items-center justify-center p-4"
        @click.self="closeLightbox"
      >
        <button
          @click="closeLightbox"
          class="absolute top-4 right-4 w-10 h-10 flex items-center justify-center rounded-full bg-white/10 hover:bg-white/20 text-white text-lg transition-colors"
        >✕</button>
        <img
          :src="lightboxImg"
          alt="Preview"
          class="max-w-full max-h-[90vh] rounded-2xl object-contain shadow-2xl"
        />
      </div>
    </Transition>

    <!-- ─── Project Modal ─── -->
    <div
      class="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm flex items-center justify-center p-4"
      @click.self="$emit('close')"
    >
      <div class="relative bg-stone-50 dark:bg-zinc-900 rounded-3xl w-full max-w-3xl max-h-[90vh] overflow-y-auto shadow-2xl">

        <!-- Close Button -->
        <button
          @click="$emit('close')"
          class="absolute top-4 right-4 z-10 w-9 h-9 flex items-center justify-center rounded-full bg-stone-200 dark:bg-zinc-800 hover:bg-stone-300 dark:hover:bg-zinc-700 text-zinc-600 dark:text-zinc-400 transition-colors"
        >✕</button>

<!-- Image Gallery -->
<div
  class="grid gap-2 p-4"
  :class="{
    'grid-cols-1': filteredImages.length === 1,
    'grid-cols-2': filteredImages.length === 2,
    'grid-cols-3': filteredImages.length >= 3,
  }"
>
  <template v-if="filteredImages.length > 0">
    <button
      v-for="(img, i) in filteredImages"
      :key="i"
      @click="openLightbox(img)"
      class="group relative w-full rounded-2xl overflow-hidden bg-stone-200 dark:bg-zinc-800 focus:outline-none"
      :class="filteredImages.length === 1 ? 'h-64' : 'h-36'"
    >
      <img
        :src="img"
        :alt="`${project.title} screenshot ${i + 1}`"
        class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-105"
      />
      <div class="absolute inset-0 bg-black/0 group-hover:bg-black/30 transition-colors duration-300 flex items-center justify-center">
        <span class="opacity-0 group-hover:opacity-100 text-white text-2xl transition-opacity duration-300">🔍</span>
      </div>
    </button>
  </template>
  <template v-else>
    <div
      v-for="i in 3"
      :key="'ph-' + i"
      class="h-36 rounded-2xl bg-stone-200 dark:bg-zinc-800 flex items-center justify-center text-zinc-400 text-sm"
    >No Image</div>
  </template>
</div>

        <!-- Content -->
        <div class="px-6 pb-6">

          <!-- Title + Tags -->
          <h2 class="font-display text-3xl font-bold text-zinc-900 dark:text-stone-100 mb-3">
            {{ project.title }}
          </h2>
          <div class="flex flex-wrap gap-2 mb-5">
            <span
              v-for="tag in project.tags"
              :key="tag"
              class="text-xs px-3 py-1 rounded-full bg-amber-100 dark:bg-amber-900/30 text-amber-700 dark:text-amber-400"
            >{{ tag }}</span>
          </div>

          <!-- Description -->
          <p class="text-zinc-600 dark:text-zinc-400 leading-relaxed mb-6 whitespace-pre-line">
            {{ project.description }}
          </p>

          <!-- What I did -->
          <div v-if="project.details?.length" class="mb-6">
            <h3 class="font-display font-bold text-zinc-900 dark:text-stone-100 mb-3">สิ่งที่ทำในโปรเจกต์นี้</h3>
            <ul class="space-y-2">
              <li
                v-for="(item, i) in project.details"
                :key="i"
                class="flex gap-3 text-zinc-600 dark:text-zinc-400"
              >
                <span class="text-amber-500 mt-0.5">▸</span>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>

          <!-- QR Code + เล่มรายงาน -->
          <div v-if="project.qr || project.reportFile" class="mb-6 p-4 rounded-2xl border border-stone-200 dark:border-zinc-800 flex flex-col sm:flex-row items-center gap-6">
            <div v-if="project.qr" class="flex flex-col items-center gap-2 shrink-0">
              <img :src="project.qr" alt="QR Code" class="w-32 h-32 object-contain rounded-xl border border-stone-200 dark:border-zinc-700 bg-white p-1" />
              <span class="text-xs text-zinc-500">สแกนดูโปรเจกต์</span>
            </div>
            <div v-if="project.reportFile" class="flex flex-col gap-2">
              <p class="text-sm font-medium text-zinc-700 dark:text-zinc-300">📄 เล่มรายงาน / เอกสารประกอบ</p>
              <p class="text-xs text-zinc-500">คลิกเพื่อดูหรือดาวน์โหลดเอกสาร</p>
              
               <a :href="project.reportFile"
                target="_blank"
                class="inline-flex items-center gap-2 px-4 py-2 bg-zinc-900 dark:bg-stone-100 text-stone-100 dark:text-zinc-900 rounded-full text-sm font-medium hover:opacity-80 transition-opacity w-fit"
              >⬇ ดาวน์โหลดเล่ม</a>
            </div>
          </div>

          <!-- Links -->
          <div class="flex gap-3 flex-wrap">
                <a
              v-if="project.github"
              :href="project.github"
              target="_blank"
              class="px-6 py-2.5 border border-zinc-300 dark:border-zinc-700 text-zinc-700 dark:text-zinc-300 rounded-full text-sm font-medium hover:bg-stone-100 dark:hover:bg-zinc-800 transition-colors"
            >GitHub</a>
          </div>

        </div>
      </div>
    </div>

  </Teleport>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>