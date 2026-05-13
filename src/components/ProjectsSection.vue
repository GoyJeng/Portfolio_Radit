<script setup>
import { ref } from 'vue'
import ProjectModal from './ProjectModal.vue'

const selectedProject = ref(null)

const projects = [
  {
    title: 'Project Driver Drowsiness Detection',
    desc: 'A computer vision application for detecting driver drowsiness using OpenCV and Flutter.',
    tags: ['OpenCV', 'Flutter', 'Python'],
    bg: 'bg-amber-100 dark:bg-amber-900/20',
    description: `ระบบตรวจจับความง่วงนอนของผู้ขับขี่แบบ Real-time ด้วย Computer Vision
โดยใช้กล้องหน้ารถตรวจจับสภาพดวงตาและแจ้งเตือนเมื่อพบความเสี่ยง`,
    details: [
      'ใช้ OpenCV ร่วมกับ dlib สำหรับ Face landmark detection',
      'คำนวณ Eye Aspect Ratio (EAR) เพื่อตรวจจับการหลับตา',
      'สร้าง Mobile App ด้วย Flutter สำหรับแสดงผลและแจ้งเตือน',
      'เชื่อมต่อ Python backend ผ่าน REST API',
    ],
    images: ['/images/Driver01.png','/images/Driver02.png','/images/Driver03.png','/images/Nice.png'],
    qr: '/images/Driver Drowsiness Detection.png',
    reportFile: '',
    demo: '',
    github: '',
  },
  {
    title: 'Project Document Submission System',
    desc: 'A web application for submitting and managing academic documents.',
    tags: ['Vue.js', 'TypeScript', 'SQL'],
    bg: 'bg-sky-100 dark:bg-sky-900/20',
    description: `ระบบรับส่งเอกสารทางวิชาการออนไลน์ สำหรับนักศึกษาและอาจารย์
รองรับการอัปโหลด ตรวจสอบสถานะ และอนุมัติเอกสารแบบ paperless`,
    details: [
      'พัฒนา Frontend ด้วย Vue.js + TypeScript',
      'ออกแบบฐานข้อมูล SQL สำหรับจัดการเอกสารและสถานะ',
      'ระบบแจ้งเตือนเมื่อเอกสารได้รับการอนุมัติหรือปฏิเสธ',
      'รองรับการอัปโหลดไฟล์ PDF และตรวจสอบความถูกต้อง',
    ],
    images: ['/images/Doc01.png','/images/Doc02.png','/images/Doc03.png'],
    qr: ['/images/Document Submission System.png'],
    reportFile: '',
    demo: '',
    github: '',
  },
  {
    title: 'Project Exam Attendance System Using Face Recognition',
    desc: 'The exam attendance system uses facial recognition and ID card verification for entry into the exam room.',
    tags: ['React', 'TypeScript', 'Node.js'],
    bg: 'bg-rose-100 dark:bg-rose-900/20',
    description: `ระบบเช็คชื่อเข้าห้องสอบด้วยการจดจำใบหน้าและตรวจสอบบัตรประจำตัว
ช่วยลดการทุจริตและเพิ่มความแม่นยำในการบันทึกการเข้าสอบ`,
    details: [
      'ใช้ Face Recognition API สำหรับยืนยันตัวตนนักศึกษา',
      'ตรวจสอบบัตรนักศึกษาด้วย OCR ควบคู่กับการจดจำใบหน้า',
      'สร้าง Dashboard ด้วย React + TypeScript สำหรับผู้คุมสอบ',
      'บันทึกและ export รายงานการเข้าสอบผ่าน Node.js backend',
    ],
    images: [''],
    qr: '',
    reportFile: '',
    demo: '',
    github: '',
  },
]
</script>

<template>
  <section id="projects" class="py-24 px-4 max-w-6xl mx-auto">
    <h2 class="font-display text-4xl sm:text-5xl font-bold text-zinc-900 dark:text-stone-100 mb-16">
      Selected Work<span class="text-amber-500">.</span>
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <button
        v-for="p in projects"
        :key="p.title"
        @click="selectedProject = p"
        class="group text-left rounded-2xl p-6 hover:-translate-y-1 transition-transform duration-300 cursor-pointer"
        :class="p.bg"
      >
        <h3 class="font-display text-xl font-bold text-zinc-900 dark:text-stone-100 mb-2 group-hover:text-amber-500 transition-colors">
          {{ p.title }}
        </h3>
        <p class="text-zinc-600 dark:text-zinc-400 text-sm mb-4">{{ p.desc }}</p>
        <div class="flex flex-wrap gap-2 mb-4">
          <span
            v-for="tag in p.tags"
            :key="tag"
            class="text-xs px-3 py-1 rounded-full bg-white/60 dark:bg-zinc-800/60 text-zinc-600 dark:text-zinc-400"
          >{{ tag }}</span>
        </div>
        <span class="text-xs text-amber-500 font-medium group-hover:underline">
View details →</span>
      </button>
    </div>
  </section>

  <ProjectModal
    v-if="selectedProject"
    :project="selectedProject"
    @close="selectedProject = null"
  />
</template>