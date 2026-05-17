<template>
  <div class="min-h-screen bg-[#f3f4f6] py-10 px-4 font-['PROMPT',_'Prompt',_sans-serif] flex flex-col items-center">
    <div class="max-w-[1000px] mx-auto w-full">
      
      <div class="mb-6">
        <NuxtLink to="/student" class="inline-flex items-center gap-2 text-gray-500 hover:text-[#1a1a40] transition-colors font-medium bg-white px-5 py-2.5 rounded-full shadow-sm hover:shadow-md mb-6 text-sm w-fit">
          <i class="bi bi-arrow-left"></i> กลับหน้าหลัก
        </NuxtLink>
        
        <h2 class="font-bold text-[30px] md:text-[34px] text-[#1a1a40] mb-3 flex items-center gap-3 tracking-tight">
          <i class="bi bi-mortarboard-fill text-[#ffc107]"></i> จัดการเอกสารยื่นขอสอบจบ
        </h2>
        <p class="text-gray-500 text-[16px] md:text-[17px]">กรุณากรอกข้อมูลและพิมพ์เอกสารทั้ง 2 ชุด เพื่อนำไปยื่นขอสอบจบโครงงาน</p>
      </div>

      <div class="w-full mb-8">
        <div class="bg-white rounded-xl p-3 px-4 md:px-5 shadow-sm border-l-4 flex flex-col md:flex-row justify-between items-start md:items-center gap-3 transition-colors duration-300"
             :class="cp2Status === 'passed' ? 'border-green-500' : (cp2Status === 'scheduled' ? 'border-blue-500' : 'border-gray-300')">
          
          <div class="flex items-start md:items-center gap-3 w-full md:w-auto">
            <div class="p-2 rounded-full shrink-0 mt-1 md:mt-0 transition-colors duration-300"
                 :class="cp2Status === 'pending' ? 'bg-gray-100 text-gray-400' : 'bg-blue-50 text-blue-500'">
              <i class="bi bi-calendar-event text-lg"></i>
            </div>
            <div>
              <div class="font-bold text-[#1a1a40] text-[15px]">กำหนดการสอบป้องกันโครงงาน (CP2)</div>
              
              <div v-if="cp2Status !== 'pending'" class="text-sm text-gray-500 flex flex-col sm:flex-row sm:items-center sm:gap-2 mt-0.5">
                <span><i class="bi bi-clock mr-1"></i> 15 ต.ค. 26 (13:00-14:30 น.)</span>
                <span class="hidden sm:inline">|</span>
                <span><i class="bi bi-geo-alt mr-1"></i> อาคาร 4 ห้อง 412</span>
              </div>
              
              <div v-else class="text-sm text-gray-400 mt-0.5">
                ยังไม่มีกำหนดการสอบ
              </div>
            </div>
          </div>

          <div class="px-3 py-1.5 rounded-full text-sm font-bold flex items-center gap-1.5 shrink-0 self-start md:self-auto transition-colors duration-300"
               :class="cp2Status === 'passed' ? 'bg-green-100 text-green-600' : (cp2Status === 'scheduled' ? 'bg-blue-100 text-blue-600' : 'bg-gray-100 text-gray-500')">
            
            <i v-if="cp2Status === 'passed'" class="bi bi-check-circle-fill"></i>
            <i v-else-if="cp2Status === 'scheduled'" class="bi bi-hourglass-split"></i>
            <i v-else class="bi bi-dash-circle-fill"></i>
            
            {{ cp2Status === 'passed' ? 'สอบผ่านเรียบร้อยแล้ว' : (cp2Status === 'scheduled' ? 'รอเข้าสอบป้องกัน' : 'ยังไม่มีผลพิจารณา') }}
          </div>

        </div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        
        <NuxtLink to="/student/cp2" class="group bg-white rounded-[24px] p-10 shadow-[0_8px_30px_rgba(0,0,0,0.04)] hover:shadow-[0_15px_40px_rgba(37,99,235,0.15)] border-[3px] border-transparent hover:border-blue-500 transition-all duration-300 flex flex-col items-center text-center relative overflow-hidden h-full">
          <div class="absolute -right-10 -top-10 w-32 h-32 bg-blue-50 rounded-full group-hover:scale-[2] transition-transform duration-700 ease-out z-0"></div>
          
          <div class="w-[85px] h-[85px] bg-blue-100 text-blue-600 rounded-full flex items-center justify-center text-[38px] mb-6 z-10 group-hover:scale-110 transition-transform duration-300 shadow-sm">
            <i class="bi bi-file-earmark-text-fill"></i>
          </div>
          
          <h3 class="font-bold text-[24px] text-[#1a1a40] mb-3 z-10">แบบขอสอบจบ (CP2)</h3>
          
          <p class="text-gray-500 text-[15px] z-10 mb-8 leading-relaxed px-4">
            เอกสารสำหรับยื่นคำร้องขอสอบป้องกันโครงงานคอมพิวเตอร์ <br class="hidden xl:block">(พิมพ์ 1 ชุด)
          </p>
          
          <div class="mt-auto bg-blue-50 text-blue-600 font-bold px-6 py-3 rounded-full text-[16px] flex items-center gap-2 z-10 group-hover:bg-blue-600 group-hover:text-white transition-colors duration-300 w-fit">
            จัดการเอกสาร <i class="bi bi-arrow-right group-hover:translate-x-1 transition-transform"></i>
          </div>
        </NuxtLink>

        <NuxtLink to="/student/cp3" class="group bg-white rounded-[24px] p-10 shadow-[0_8px_30px_rgba(0,0,0,0.04)] hover:shadow-[0_15px_40px_rgba(16,185,129,0.15)] border-[3px] border-transparent hover:border-emerald-500 transition-all duration-300 flex flex-col items-center text-center relative overflow-hidden h-full">
          <div class="absolute -right-10 -top-10 w-32 h-32 bg-emerald-50 rounded-full group-hover:scale-[2] transition-transform duration-700 ease-out z-0"></div>
          
          <div class="w-[85px] h-[85px] bg-emerald-100 text-emerald-600 rounded-full flex items-center justify-center text-[38px] mb-6 z-10 group-hover:scale-110 transition-transform duration-300 shadow-sm">
            <i class="bi bi-file-earmark-check-fill"></i>
          </div>
          
          <h3 class="font-bold text-[24px] text-[#1a1a40] mb-3 z-10">แบบประเมินสอบ (CP3)</h3>
          
          <p class="text-gray-500 text-[15px] z-10 mb-8 leading-relaxed px-4">
            เอกสารสำหรับให้คณะกรรมการบันทึกผลการประเมินการสอบป้องกัน <br class="hidden xl:block">(พิมพ์ 1 ชุด)
          </p>
          
          <div class="mt-auto bg-emerald-50 text-emerald-600 font-bold px-6 py-3 rounded-full text-[16px] flex items-center gap-2 z-10 group-hover:bg-emerald-500 group-hover:text-white transition-colors duration-300 w-fit">
            จัดการเอกสาร <i class="bi bi-arrow-right group-hover:translate-x-1 transition-transform"></i>
          </div>
        </NuxtLink>

      </div>

    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

useHead({
  title: 'จัดการเอกสารยื่นขอสอบจบ (CP2 & CP3)'
})

// ================= ตัวแปรสลับสถานะสอบจบ (เปลี่ยนเพื่อเทส UI หน้าเว็บได้เลยครับ) =================
// 'pending' = ยังไม่ยื่น/รออาจารย์นัดเวลา, 'scheduled' = นัดวันสอบจบแล้ว, 'passed' = สอบผ่านแล้ว
const cp2Status = ref('pending')
</script>