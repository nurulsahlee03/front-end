<template>
  <div class="flex flex-col min-h-screen bg-[#f8f9fa] font-['Prompt']">
    
    <nav class="sticky top-0 z-50 bg-gradient-to-r from-[#1a1a40] to-[#302b63] py-3 shadow-[0_4px_20px_rgba(0,0,0,0.1)]">
      <div class="max-w-[1140px] mx-auto px-4 flex flex-wrap items-center justify-between">
        
        <NuxtLink
          to="/student"
          class="text-white font-bold text-[1.4rem] flex items-center gap-2 no-underline"
        >
          <i class="bi bi-mortarboard-fill"></i> Student Panel
        </NuxtLink>

        <button
          @click="isMenuOpen = !isMenuOpen"
          class="lg:hidden text-white text-2xl focus:outline-none"
        >
          <i class="bi" :class="isMenuOpen ? 'bi-x-lg' : 'bi-list'"></i>
        </button>

        <div
          :class="isMenuOpen ? 'flex' : 'hidden'"
          class="w-full lg:flex lg:w-auto lg:flex-grow flex-col lg:flex-row items-start lg:items-center mt-4 lg:mt-0"
        >
          <ul class="flex flex-col lg:flex-row lg:mr-auto lg:ml-8 w-full lg:w-auto gap-2 lg:gap-1 mb-4 lg:mb-0">
            <li>
              <NuxtLink
                to="/procedures"
                class="flex items-center gap-1 text-white/85 hover:text-white hover:bg-white/15 px-[18px] py-[8px] rounded-full transition-all duration-300 font-medium text-[0.95rem]"
              >
                <i class="bi bi-diagram-3-fill"></i> ขั้นตอนการทำโครงงาน
              </NuxtLink>
            </li>

            <li v-if="isApproved">
              <NuxtLink
                to="/student"
                class="flex items-center gap-1 text-white hover:bg-white/15 px-[18px] py-[8px] rounded-full transition-all duration-300 font-medium text-[0.95rem]"
              >
                <i class="bi bi-folder-fill"></i> โครงงาน
              </NuxtLink>
            </li>

            <li>
              <NuxtLink
                to="/senior-projects"
                class="flex items-center gap-1 text-white/85 hover:text-white hover:bg-white/15 px-[18px] py-[8px] rounded-full transition-all duration-300 font-medium text-[0.95rem]"
              >
                <i class="bi bi-collection-play-fill"></i> โครงงานรุ่นพี่
              </NuxtLink>
            </li>
            
            <li>
              <a
                href="/thesis_manual.pdf"
                target="_blank"
                class="flex items-center gap-1 text-white/85 hover:text-white hover:bg-white/15 px-[18px] py-[8px] rounded-full transition-all duration-300 font-medium text-[0.95rem]"
              >
                <i class="bi bi-book-half"></i> คู่มือทำเล่ม
              </a>
            </li>
          </ul>

          <div class="flex flex-col lg:flex-row items-start lg:items-center gap-4 lg:gap-0 w-full lg:w-auto">
            <div class="hidden lg:flex items-center gap-[10px] text-white bg-white/10 pr-[15px] pl-[5px] py-[5px] rounded-full lg:mr-[15px]">
              <div class="w-[32px] h-[32px] bg-white text-[#1a1a40] rounded-full flex items-center justify-center font-bold text-[0.9rem]">
                น
              </div>
              <span class="text-[0.9rem]">นางสาวตัวอย่าง ใจดี</span>
            </div>

            <NuxtLink
              to="/login"
              class="flex items-center gap-1 text-white border border-white/30 hover:bg-[#dc3545] hover:border-[#dc3545] px-[18px] py-[6px] rounded-full text-[0.85rem] transition-colors duration-300 w-fit"
            >
              <i class="bi bi-box-arrow-right"></i> Logout
            </NuxtLink>
          </div>
        </div>
      </div>
    </nav>

    <main class="flex-grow w-full py-6">
      <slot />
    </main>

    <footer class="bg-[#1a1a40] text-white mt-auto">
      <div class="max-w-[1140px] mx-auto px-4 py-10">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          
          <div class="lg:col-span-2">
            <h5 class="uppercase font-bold text-[#ffc107] mb-4 text-lg flex items-center gap-2">
              <i class="bi bi-mortarboard-fill"></i> Computer Science Project
            </h5>
            <p class="text-sm text-gray-300 leading-relaxed">
              ระบบบริหารจัดการโครงงานคอมพิวเตอร์<br />
              สาขาวิชาวิทยาการคอมพิวเตอร์ มหาวิทยาลัยราชภัฏบ้านสมเด็จเจ้าพระยา
            </p>
          </div>

          <div>
            <h5 class="uppercase font-bold text-base mb-4">เมนูหลัก</h5>
            <ul class="text-sm space-y-2">
              <li>
                <NuxtLink to="/student" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">หน้าหลัก</NuxtLink>
              </li>
              <li>
                <NuxtLink to="/procedures" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">ขั้นตอนโครงงาน</NuxtLink>
              </li>
              <li>
                <NuxtLink to="/senior-projects" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">โครงงานรุ่นพี่</NuxtLink>
              </li>
              <li>
                <a
                  href="/thesis_manual.pdf"
                  target="_blank"
                  class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors"
                >
                  คู่มือทำเล่มบัณฑิตนิพนธ์
                </a>
              </li>
            </ul>
          </div>

          <div>
            <h5 class="uppercase font-bold text-base mb-4">ติดต่อ</h5>
            <ul class="text-sm space-y-3">
              <li class="flex items-start gap-2 text-gray-300">
                <i class="bi bi-geo-alt-fill mt-1"></i> อาคาร 4 ห้อง 412 สาขาวิชาวิทยาการคอมพิวเตอร์
              </li>
              <li class="flex items-center gap-2 text-gray-300">
                <i class="bi bi-telephone-fill"></i> 02-xxx-xxxx
              </li>
              <li class="text-[#ffc107] mt-3 font-medium">ผู้จัดทำ: คุณหนูเต้ย (Front-end)</li>
            </ul>
          </div>
        </div>
      </div>

      <div class="bg-black/20 text-center p-4 text-sm">
        © 2026 Copyright:
        <a href="#" class="text-white hover:text-[#ffc107] hover:underline transition-colors">BSRU Computer Science</a>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";

const isMenuOpen = ref(false);
const isApproved = ref(false);

useHead({
  titleTemplate: "%s | BSRU Computer Project",
  link: [
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap",
    },
    {
      rel: "stylesheet",
      href: "https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css",
    },
  ],
});
</script>