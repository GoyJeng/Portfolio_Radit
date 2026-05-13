<script setup>
const skills = [
  { name: 'Vue.js', level: 90 },
  { name: 'Tailwind CSS', level: 85 },
  { name: 'JavaScript', level: 70 },
  { name: 'Node.js', level: 68 },
  { name: 'Python', level: 75 },
  { name: 'SQL', level: 80 },
  { name: 'Prompt Engineering', level: 300 },
]
</script>

<template>
  <section id="skills" class="py-24 px-4 bg-stone-100 dark:bg-zinc-900">
    <div class="max-w-4xl mx-auto">
      <h2 class="font-display text-4xl sm:text-5xl font-bold text-zinc-900 dark:text-stone-100 mb-16">
        Skills<span class="text-amber-500">.</span>
      </h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
        <div v-for="skill in skills" :key="skill.name">
          <div class="flex justify-between mb-2">
            <span class="text-zinc-700 dark:text-zinc-300 font-medium">{{ skill.name }}</span>
            <span class="text-zinc-500 dark:text-zinc-500 text-sm">{{ skill.level }}%</span>
          </div>
          <div class="h-2 bg-stone-200 dark:bg-zinc-800 rounded-full overflow-hidden">
            <div
              class="h-full bg-amber-500 rounded-full transition-all duration-700"
              :style="{ width: skill.level + '%' }"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>