<script setup>
const projects = [
  {
    title: 'Project One',
    desc: 'A full-stack web application built with Vue and Node.js.',
    tags: ['Vue', 'Node.js', 'MongoDB'],
    link: '#',
    bg: 'bg-amber-100 dark:bg-amber-900/20'
  },
  {
    title: 'Project Two',
    desc: 'Mobile-first e-commerce UI with smooth animations.',
    tags: ['React', 'Tailwind', 'Stripe'],
    link: '#',
    bg: 'bg-sky-100 dark:bg-sky-900/20'
  },
  {
    title: 'Project Three',
    desc: 'Dashboard for real-time data visualization.',
    tags: ['D3.js', 'TypeScript', 'REST API'],
    link: '#',
    bg: 'bg-rose-100 dark:bg-rose-900/20'
  },
]
</script>

<template>
  <section id="projects" class="py-24 px-4 max-w-6xl mx-auto">
    <h2 class="font-display text-4xl sm:text-5xl font-bold text-zinc-900 dark:text-stone-100 mb-16">
      Selected Work<span class="text-amber-500">.</span>
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      
        <a v-for="p in projects"
        :key="p.title"
        :href="p.link"
        class="group rounded-2xl p-6 hover:-translate-y-1 transition-transform duration-300"
        :class="p.bg"
      >
        <h3 class="font-display text-xl font-bold text-zinc-900 dark:text-stone-100 mb-2 group-hover:text-amber-500 transition-colors">
          {{ p.title }}
        </h3>
        <p class="text-zinc-600 dark:text-zinc-400 text-sm mb-4">{{ p.desc }}</p>
        <div class="flex flex-wrap gap-2">
          <span
            v-for="tag in p.tags"
            :key="tag"
            class="text-xs px-3 py-1 rounded-full bg-white/60 dark:bg-zinc-800/60 text-zinc-600 dark:text-zinc-400"
          >{{ tag }}</span>
        </div>
      </a>
    </div>
  </section>
</template>