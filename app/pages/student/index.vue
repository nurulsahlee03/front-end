<template>
  <div class="w-full">
    
    <div v-if="isApproved" class="bg-white rounded-[20px] shadow-[0_4px_25px_rgba(0,0,0,0.05)] p-[40px] max-w-[800px] mx-auto my-[40px]">
      <div class="text-center mb-[40px]">
        <h3 class="font-bold text-[24px] mb-1 text-[#212529]">สถานะการดำเนินงาน</h3>
        <p class="text-[#6c757d]">ติดตามความคืบหน้าบัณฑิตนิพนธ์</p>
      </div>

      <div class="flex items-center relative pb-[40px]">
        <div class="w-[50px] h-[50px] rounded-full flex items-center justify-center font-bold text-[18px] border-2 border-[#0d6efd] bg-[#0d6efd] text-white z-10 shrink-0">1</div>
        <div class="absolute left-[24px] top-[50px] bottom-0 w-[2px] bg-[#0d6efd]"></div>
        <div class="flex-grow ml-[25px] flex flex-col sm:flex-row sm:items-center justify-between gap-2">
          <div class="font-semibold text-[16px] text-[#212529]">ยื่นขอสอบหัวข้อ (CP1)</div>
          <div class="flex items-center">
            <div class="text-[14px] font-semibold mr-[20px] text-[#0d6efd]">กำลังดำเนินการ</div>
            <NuxtLink to="/cp1" class="w-[40px] h-[40px] rounded-full border border-[#0d6efd] bg-white flex items-center justify-center text-[#0d6efd] hover:bg-[#0d6efd] hover:text-white transition-colors duration-200 shadow-sm">
              <i class="bi bi-pencil-square"></i>
            </NuxtLink>
          </div>
        </div>
      </div>

      <div class="flex items-center relative pb-[40px]">
        <div class="w-[50px] h-[50px] rounded-full flex items-center justify-center font-bold text-[18px] border-2 border-[#0d6efd] bg-[#0d6efd] text-white z-10 shrink-0">2</div>
        <div class="absolute left-[24px] top-[50px] bottom-0 w-[2px] bg-[#0d6efd]"></div>
        <div class="flex-grow ml-[25px] flex flex-col sm:flex-row sm:items-center justify-between gap-2">
          <div class="font-semibold text-[16px] text-[#212529]">พัฒนาโปรแกรม</div>
          <div class="flex items-center">
            <div class="text-[14px] font-semibold mr-[20px] text-[#0d6efd]">กำลังดำเนินการ</div>
            <NuxtLink to="/progress" class="w-[40px] h-[40px] rounded-full border border-[#0d6efd] bg-white flex items-center justify-center text-[#0d6efd] hover:bg-[#0d6efd] hover:text-white transition-colors duration-200 shadow-sm">
              <i class="bi bi-plus-lg"></i>
            </NuxtLink>
          </div>
        </div>
      </div>

      <div class="flex items-center relative pb-[40px]">
        <div class="w-[50px] h-[50px] rounded-full flex items-center justify-center font-bold text-[18px] border-2 border-[#0d6efd] bg-[#0d6efd] text-white z-10 shrink-0">3</div>
        <div class="absolute left-[24px] top-[50px] bottom-0 w-[2px] bg-[#0d6efd]"></div>
        <div class="flex-grow ml-[25px] flex flex-col sm:flex-row sm:items-center justify-between gap-2">
          <div class="font-semibold text-[16px] text-[#212529]">เล่มบัณฑิตนิพนธ์</div>
          <div class="flex items-center">
            <div class="text-[14px] font-semibold mr-[20px] text-[#0d6efd]">กำลังดำเนินการ</div>
            <NuxtLink to="/thesis" class="w-[40px] h-[40px] rounded-full border border-[#0d6efd] bg-white flex items-center justify-center text-[#0d6efd] hover:bg-[#0d6efd] hover:text-white transition-colors duration-200 shadow-sm">
              <i class="bi bi-plus-lg"></i>
            </NuxtLink>
          </div>
        </div>
      </div>

      <div class="flex items-center relative pb-[40px]">
        <div class="w-[50px] h-[50px] rounded-full flex items-center justify-center font-bold text-[18px] border-2 border-[#0d6efd] bg-white text-[#0d6efd] z-10 shrink-0">4</div>
        <div class="absolute left-[24px] top-[50px] bottom-0 w-[2px] bg-[#e9ecef]"></div>
        <div class="flex-grow ml-[25px] flex flex-col sm:flex-row sm:items-center justify-between gap-2">
          <div class="font-semibold text-[16px] text-[#212529]">ยื่นขอสอบจบ (CP2)</div>
          <div class="flex items-center">
            <div class="text-[14px] font-semibold mr-[20px] text-[#0d6efd]">คลิกเพื่อยื่นขอสอบ</div>
            <NuxtLink to="/cp2" class="w-[40px] h-[40px] rounded-full border border-[#0d6efd] bg-white flex items-center justify-center text-[#0d6efd] hover:bg-[#0d6efd] hover:text-white transition-colors duration-200 shadow-sm">
              <i class="bi bi-plus-lg"></i>
            </NuxtLink>
          </div>
        </div>
      </div>

      <div class="flex items-center relative">
        <div class="w-[50px] h-[50px] rounded-full flex items-center justify-center font-bold text-[18px] border-2 border-[#0d6efd] bg-white text-[#0d6efd] z-10 shrink-0">5</div>
        <div class="flex-grow ml-[25px] flex flex-col sm:flex-row sm:items-center justify-between gap-2">
          <div class="font-semibold text-[16px] text-[#212529]">ส่งเล่มและโปรแกรม</div>
          <div class="flex items-center">
            <div class="text-[14px] font-semibold mr-[20px] text-[#0d6efd]">คลิกเพื่อส่งงาน</div>
            <NuxtLink to="/final-submit" class="w-[40px] h-[40px] rounded-full border border-[#0d6efd] bg-white flex items-center justify-center text-[#0d6efd] hover:bg-[#0d6efd] hover:text-white transition-colors duration-200 shadow-sm">
              <i class="bi bi-plus-lg"></i>
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>

    <div v-else class="bg-white rounded-[20px] shadow-[0_4px_25px_rgba(0,0,0,0.05)] p-[60px] max-w-[800px] mx-auto my-[60px] text-center">
      <div class="w-[100px] h-[100px] bg-[#fff3cd] text-[#ffc107] rounded-full flex items-center justify-center mx-auto mb-6">
        <i class="bi bi-hourglass-split text-[50px]"></i>
      </div>
      <h3 class="font-bold text-[24px] text-[#1a1a40] mb-3">รอการอนุมัติจากผู้ดูแลระบบ</h3>
      <p class="text-[#6c757d] mb-8 leading-relaxed max-w-[500px] mx-auto">
        บัญชีของคุณกำลังรอการตรวจสอบจากแอดมิน<br>
        เมื่อได้รับการอนุมัติแล้ว คุณถึงจะสามารถเริ่มต้นยื่นเสนอหัวข้อและทำโครงงานได้ครับ
      </p>
      
      <div class="flex flex-col sm:flex-row flex-wrap justify-center gap-4">
        
        <NuxtLink to="/procedures" class="border-2 border-[#1a1a40] text-[#1a1a40] px-6 py-3 rounded-full hover:bg-[#1a1a40] hover:text-white transition-colors font-medium flex items-center justify-center gap-2">
          <i class="bi bi-diagram-3"></i> ขั้นตอนการทำโครงงาน
        </NuxtLink>

        <NuxtLink to="/senior-projects" class="border-2 border-[#1a1a40] text-[#1a1a40] px-6 py-3 rounded-full hover:bg-[#1a1a40] hover:text-white transition-colors font-medium flex items-center justify-center gap-2">
          <i class="bi bi-search"></i> ดูโครงงานรุ่นพี่
        </NuxtLink>

        <a href="/thesis_manual.pdf" target="_blank" class="border-2 border-[#1a1a40] text-[#1a1a40] px-6 py-3 rounded-full hover:bg-[#1a1a40] hover:text-white transition-colors font-medium flex items-center justify-center gap-2">
          <i class="bi bi-book"></i> อ่านคู่มือทำเล่ม
        </a>
        
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

useHead({
  title: 'หน้าหลัก'
})

// ตัวแปรจำลองสถานะ: เปลี่ยนเป็น true หน้าเว็บจะเปลี่ยนเป็น Timeline ทันที
const isApproved = ref(false) 
</script>