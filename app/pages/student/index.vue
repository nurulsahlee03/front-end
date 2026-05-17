<template>
  <div class="w-full font-['PROMPT'] flex justify-center items-stretch min-h-[calc(100vh-130px)]">
    
    <div v-if="isApproved" class="bg-white rounded-[24px] shadow-[0_8px_30px_rgba(0,0,0,0.04)] p-8 md:p-10 max-w-[1200px] w-full border border-gray-50 flex flex-col">
      
      <div class="text-center mb-10 shrink-0">
        <h3 class="font-bold text-[32px] text-[#1a1a40] mb-2 tracking-tight">สถานะการดำเนินงาน</h3>
        <p class="text-gray-500 text-[16px]">ติดตามและจัดการขั้นตอนความคืบหน้าโครงงานคอมพิวเตอร์ของคุณ</p>
      </div>

      <div class="relative px-2 md:px-8 flex-grow flex flex-col">
        <div v-for="(step, index) in steps" :key="step.id" class="flex items-start relative flex-1 group">
          
          <div v-if="index !== steps.length - 1" 
               class="absolute left-[27px] top-[56px] bottom-0 w-[2px] transition-all duration-500 z-0" 
               :class="step.isCompleted ? 'bg-blue-500' : 'bg-gray-200 group-hover:bg-gray-300'">
          </div>

          <div 
            class="w-[56px] h-[56px] rounded-full flex items-center justify-center font-bold text-[20px] border-[2px] z-10 shrink-0 transition-all duration-300 group-hover:scale-110 shadow-sm mt-1"
            :class="step.isLocked ? 'border-gray-200 bg-gray-50 text-gray-400' : (step.isCompleted ? 'border-blue-500 bg-blue-500 text-white' : 'border-[#1a1a40] bg-[#1a1a40] text-white')"
          >
            <i v-if="step.isCompleted" class="bi bi-check-lg text-[26px]"></i>
            <span v-else>{{ step.id }}</span>
          </div>

          <div class="flex-grow ml-8 flex flex-row items-center justify-between min-h-[60px]">
            
            <div class="flex flex-col">
              <div class="font-bold text-[22px] mb-0.5 transition-colors duration-300" :class="step.isLocked ? 'text-gray-400' : 'text-[#1a1a40] group-hover:text-blue-600'">
                {{ step.title }}
              </div>
              <div class="text-[15px] font-medium opacity-90" :class="step.statusColor">
                {{ step.statusText }}
              </div>
            </div>
            
            <div class="flex items-center">
              <div v-if="step.isLocked" class="w-[50px] h-[50px] rounded-[14px] border-2 border-gray-100 bg-gray-50 flex items-center justify-center text-gray-300 cursor-not-allowed">
                <i class="bi bi-lock-fill text-lg"></i>
              </div>

              <NuxtLink v-else :to="step.link" 
                class="w-[50px] h-[50px] rounded-[14px] border-2 bg-white flex items-center justify-center transition-all duration-300 shadow-sm hover:shadow-md group-hover:-translate-y-1" 
                :class="step.isCompleted ? 'border-blue-500 text-blue-500 hover:bg-blue-500 hover:text-white' : 'border-[#1a1a40] text-[#1a1a40] hover:bg-[#1a1a40] hover:text-white'">
                <i class="bi text-xl" :class="step.icon"></i>
              </NuxtLink>
            </div>

          </div>
        </div>
      </div>
    </div>

    <div v-else class="bg-white rounded-[24px] shadow-[0_8px_30px_rgba(0,0,0,0.04)] p-[60px] max-w-[800px] w-full mx-auto text-center border border-gray-50 flex flex-col items-center justify-center">
      <div class="w-[100px] h-[100px] bg-[#fff3cd] text-[#ffc107] rounded-full flex items-center justify-center mx-auto mb-6 shadow-inner">
        <i class="bi bi-hourglass-split text-[50px] animate-pulse"></i>
      </div>
      <h3 class="font-bold text-[26px] text-[#1a1a40] mb-3">รอการอนุมัติจากผู้ดูแลระบบ</h3>
      <p class="text-[#6c757d] text-[15px] leading-relaxed max-w-[500px] mx-auto">
        บัญชีของคุณกำลังรอการตรวจสอบจากแอดมิน<br>
        เมื่อได้รับการอนุมัติแล้ว คุณถึงจะสามารถเริ่มต้นยื่นเสนอหัวข้อและทำโครงงานได้ครับ
      </p>
    </div>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

useHead({
  title: 'สถานะการดำเนินงาน | โครงงานของฉัน'
})

// ================= เปิดให้ผ่านทุกด่านเพื่อทดสอบ UI =================
const isApproved = ref(true) 
const isCp1Passed = ref(true) 
const isProgressAndThesisPassed = ref(true) 
const isCp2Passed = ref(true) 

// ================= คำนวณสถานะ 5 ขั้นตอน =================
const steps = computed(() => [
  {
    id: 1,
    title: 'การสอบพิจารณาหัวข้อโครงงาน (CP1)',
    statusText: isCp1Passed.value ? 'ผ่านการพิจารณาแล้ว' : 'อยู่ระหว่างการดำเนินงาน',
    statusColor: isCp1Passed.value ? 'text-green-600' : 'text-[#1a1a40]',
    icon: isCp1Passed.value ? 'bi-eye-fill' : 'bi-pencil-square',
    link: '/student/cp1',
    isLocked: false, 
    isCompleted: isCp1Passed.value
  },
  {
    id: 2,
    title: 'พัฒนาโปรแกรมและระบบสารสนเทศ',
    statusText: isCp1Passed.value ? (isProgressAndThesisPassed.value ? 'ผ่านการตรวจประเมินแล้ว' : 'อยู่ระหว่างการพัฒนา') : 'รอผ่านการอนุมัติหัวข้อ (CP1)',
    statusColor: isCp1Passed.value ? (isProgressAndThesisPassed.value ? 'text-green-600' : 'text-blue-600') : 'text-gray-400',
    icon: isProgressAndThesisPassed.value ? 'bi-eye-fill' : 'bi-plus-lg',
    link: '/student/progress',
    isLocked: !isCp1Passed.value,
    isCompleted: isProgressAndThesisPassed.value
  },
  {
    id: 3,
    title: 'จัดทำเล่มบัณฑิตนิพนธ์',
    statusText: isCp1Passed.value ? (isProgressAndThesisPassed.value ? 'ผ่านการตรวจประเมินแล้ว' : 'อยู่ระหว่างการจัดทำเล่ม') : 'รอผ่านการอนุมัติหัวข้อ (CP1)',
    statusColor: isCp1Passed.value ? (isProgressAndThesisPassed.value ? 'text-green-600' : 'text-blue-600') : 'text-gray-400',
    icon: isProgressAndThesisPassed.value ? 'bi-eye-fill' : 'bi-plus-lg',
    link: '/student/thesis',
    isLocked: !isCp1Passed.value,
    isCompleted: isProgressAndThesisPassed.value
  },
  {
    id: 4,
    title: 'การสอบจบโครงงาน (CP2, CP3)', 
    statusText: isProgressAndThesisPassed.value ? (isCp2Passed.value ? 'ผ่านการสอบจบโครงงานแล้ว' : 'คลิกเพื่อจัดการเอกสารการสอบ') : 'รอผ่านขั้นตอนพัฒนาและเล่มเอกสาร',
    statusColor: isProgressAndThesisPassed.value ? (isCp2Passed.value ? 'text-green-600' : 'text-blue-600') : 'text-gray-400',
    icon: isCp2Passed.value ? 'bi-eye-fill' : 'bi-folder2-open', 
    link: '/student/exam-request', 
    isLocked: !isProgressAndThesisPassed.value,
    isCompleted: isCp2Passed.value
  },
  {
    id: 5,
    title: 'ส่งมอบเล่มฉบับสมบูรณ์และโปรแกรม',
    statusText: isCp2Passed.value ? 'รอดำเนินการส่งมอบงาน' : 'รอผ่านการสอบป้องกันโครงงาน (CP2)',
    statusColor: isCp2Passed.value ? 'text-blue-600' : 'text-gray-400',
    icon: 'bi-cloud-arrow-up-fill',
    link: '/student/final-submit',
    isLocked: !isCp2Passed.value,
    isCompleted: false 
  }
])
</script>