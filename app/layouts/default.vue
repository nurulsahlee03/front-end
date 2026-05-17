<template>
  <div class="flex flex-col min-h-screen bg-[#f8f9fa] font-['PROMPT']">
    
   <nav class="sticky top-0 z-50 bg-[#252243] py-3 shadow-[0_4px_20px_rgba(0,0,0,0.1)]">
      <div class="w-full px-4 md:px-8 xl:px-10 flex items-center justify-between relative">
        
        <div class="flex items-center xl:w-[25%] justify-start shrink-0">
          <NuxtLink to="/student" class="text-white font-bold text-[1.4rem] flex items-center gap-2 no-underline">
            <i class="bi bi-mortarboard-fill text-[#ffc107]"></i> Student Panel
          </NuxtLink>
        </div>

        <button @click="isMenuOpen = !isMenuOpen" class="xl:hidden text-white text-2xl focus:outline-none transition-transform active:scale-95">
          <i class="bi" :class="isMenuOpen ? 'bi-x-lg' : 'bi-list'"></i>
        </button>

        <div :class="isMenuOpen ? 'flex' : 'hidden'" class="w-full xl:flex xl:flex-1 flex-col xl:flex-row absolute xl:static top-full left-0 bg-[#252243] xl:bg-transparent px-4 md:px-8 xl:px-0 py-6 xl:py-0 mt-3 xl:mt-0 shadow-2xl xl:shadow-none border-t border-white/10 xl:border-none gap-6 xl:gap-0 rounded-b-2xl xl:rounded-none z-40">
          
          <ul class="flex flex-col xl:flex-row gap-2 w-full xl:w-auto xl:mx-auto xl:justify-center">
            <li class="w-full xl:w-auto">
              <NuxtLink to="/procedures" active-class="bg-white/20 text-white" class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-[15px] py-[10px] xl:py-[8px] rounded-xl xl:rounded-full transition-all duration-300 font-medium text-[0.95rem] whitespace-nowrap w-full xl:w-auto">
                <i class="bi bi-diagram-3-fill"></i> กระบวนการจัดทำโครงงาน
              </NuxtLink>
            </li>

            <li v-if="isApproved" class="w-full xl:w-auto">
              <NuxtLink to="/student" active-class="bg-white/20 text-white" class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-[15px] py-[10px] xl:py-[8px] rounded-xl xl:rounded-full transition-all duration-300 font-medium text-[0.95rem] whitespace-nowrap w-full xl:w-auto">
                <i class="bi bi-folder-fill"></i> จัดการโครงงาน
              </NuxtLink>
            </li>

            <li class="w-full xl:w-auto">
              <NuxtLink to="/senior-projects" active-class="bg-white/20 text-white" class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-[15px] py-[10px] xl:py-[8px] rounded-xl xl:rounded-full transition-all duration-300 font-medium text-[0.95rem] whitespace-nowrap w-full xl:w-auto">
                <i class="bi bi-collection-play-fill"></i> ฐานข้อมูลบัณฑิตนิพนธ์
              </NuxtLink>
            </li>

            <li class="w-full xl:w-auto">
              <a href="/thesis_manual.pdf" target="_blank" class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-[15px] py-[10px] xl:py-[8px] rounded-xl xl:rounded-full transition-all duration-300 font-medium text-[0.95rem] whitespace-nowrap w-full xl:w-auto">
                <i class="bi bi-book-half"></i> คู่มือจัดทำบัณฑิตนิพนธ์
              </a>
            </li>
          </ul>

          <div class="flex flex-col xl:flex-row items-start xl:items-center xl:justify-end gap-4 xl:gap-3 w-full xl:w-[25%] shrink-0 border-t border-white/10 xl:border-none pt-4 xl:pt-0">
            
            <NuxtLink to="/student/profile" class="flex items-center gap-[10px] text-white bg-white/10 hover:bg-white/20 cursor-pointer transition-colors duration-300 pr-[18px] pl-[6px] py-[8px] xl:py-[6px] rounded-full no-underline whitespace-nowrap w-max">
              <div class="w-[32px] h-[32px] bg-white text-[#1a1a40] rounded-full flex items-center justify-center font-bold text-[0.9rem]">
                น
              </div>
              <span class="text-[0.95rem] font-medium hidden xl:inline-block 2xl:inline-block">นางสาวตัวอย่าง ใจดี</span>
            </NuxtLink>

            <NuxtLink to="/login" class="flex items-center justify-center gap-2 text-white border border-white/30 hover:bg-[#dc3545] hover:border-[#dc3545] px-[20px] py-[10px] xl:py-[8px] rounded-full text-[0.9rem] font-medium transition-colors duration-300 w-full xl:w-fit whitespace-nowrap">
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
              <li><NuxtLink to="/student" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">หน้าหลัก</NuxtLink></li>
              <li><NuxtLink to="/procedures" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">กระบวนการจัดทำโครงงาน</NuxtLink></li>
              <li><NuxtLink to="/senior-projects" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">ฐานข้อมูลบัณฑิตนิพนธ์</NuxtLink></li>
              <li><a href="/thesis_manual.pdf" target="_blank" class="text-gray-300 hover:text-[#ffc107] hover:underline transition-colors">คู่มือจัดทำบัณฑิตนิพนธ์</a></li>
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

// รวมตัวแปรทั้งหมดไว้ก้อนเดียว
const isMenuOpen = ref(false);
const isApproved = ref(true);

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