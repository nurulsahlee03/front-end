<template>
  <div class="min-h-[calc(100vh-140px)] py-6 px-4 font-['PROMPT'] bg-[#f3f4f6] flex flex-col justify-center items-center">
    
    <div class="max-w-[1350px] w-full">
      
      <div class="mb-8">
        <NuxtLink to="/student" class="flex items-center gap-2 text-gray-500 hover:text-[#1a1a40] transition-colors mb-4 font-medium w-fit bg-white px-5 py-2.5 rounded-full shadow-sm text-sm">
          <i class="bi bi-arrow-left"></i> กลับหน้าหลัก
        </NuxtLink>
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
          <div>
            <h2 class="font-bold text-[30px] md:text-[34px] text-[#1a1a40] flex items-center gap-4 tracking-tight">
              <div class="w-14 h-14 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center shadow-sm shrink-0">
                <i class="bi bi-box-seam-fill text-[26px]"></i>
              </div>
              ส่งเล่มและโปรแกรมฉบับสมบูรณ์
            </h2>
            <p class="text-gray-500 mt-2 text-[16px] ml-[72px]">ขั้นตอนสุดท้าย: อัปโหลดไฟล์เอกสารรูปเล่มและซอร์สโค้ดโปรแกรมฉบับสมบูรณ์</p>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-[32px] p-10 lg:p-14 shadow-[0_10px_40px_rgba(0,0,0,0.05)] border border-gray-50">
        
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 lg:gap-0 lg:divide-x-2 divide-gray-100">
          
          <div class="flex flex-col lg:pr-14 h-full">
            <h3 class="font-bold text-[20px] text-[#1a1a40] mb-3 flex items-center gap-3">
              <span class="w-10 h-10 rounded-full bg-blue-100 text-blue-600 flex items-center justify-center text-[16px] shadow-sm border-2 border-white">1</span>
              แนบไฟล์รูปเล่มปริญญานิพนธ์
            </h3>
            <label class="block text-[15px] font-medium text-gray-600 mb-4 ml-[52px]">ไฟล์รูปเล่มฉบับสมบูรณ์ (รองรับเฉพาะไฟล์ .pdf)</label>
            
            <div class="ml-0 lg:ml-[52px] flex-grow border-[3px] border-dashed border-gray-200 rounded-[24px] p-8 flex flex-col items-center justify-center hover:bg-blue-50/50 hover:border-blue-400 transition-all duration-300 text-center relative group min-h-[280px]">
              <input type="file" accept=".pdf" @change="handleDocumentUpload" class="absolute inset-0 w-full h-full opacity-0 cursor-pointer z-10">
              
              <div v-if="!form.documentName" class="text-gray-500 group-hover:scale-105 transition-transform duration-300">
                <i class="bi bi-file-earmark-pdf-fill text-[70px] mb-3 block text-red-500 drop-shadow-sm"></i>
                <p class="text-[18px] font-bold text-[#1a1a40]">คลิกเพื่อเลือกไฟล์ หรือลากมาวาง</p>
                <p class="text-[14px] text-gray-400 mt-1.5">ขนาดไฟล์ไม่เกิน 20MB</p>
              </div>
              
              <div v-else class="text-green-600 font-bold text-[18px] flex items-center justify-center gap-3 bg-green-50 p-5 rounded-2xl border border-green-200 w-full shadow-sm">
                <i class="bi bi-check-circle-fill text-[28px] shrink-0"></i> 
                <span class="truncate">{{ form.documentName }}</span>
              </div>
            </div>
          </div>

          <div class="flex flex-col lg:pl-14 h-full">
            <h3 class="font-bold text-[20px] text-[#1a1a40] mb-3 flex items-center gap-3">
              <span class="w-10 h-10 rounded-full bg-emerald-100 text-emerald-600 flex items-center justify-center text-[16px] shadow-sm border-2 border-white">2</span>
              แนบซอร์สโค้ดโปรแกรม
            </h3>
            
            <div class="ml-0 lg:ml-[52px] flex flex-col h-full space-y-6">
              
              <div>
                <label class="block text-[15px] font-medium text-gray-600 mb-3">ไฟล์ Source Code (รองรับไฟล์ .zip, .rar)</label>
                <div class="border-[3px] border-dashed border-gray-200 rounded-[24px] p-6 hover:bg-emerald-50/50 hover:border-emerald-400 transition-all duration-300 text-center relative group min-h-[150px] flex items-center justify-center">
                  <input type="file" accept=".zip,.rar" @change="handleProgramUpload" class="absolute inset-0 w-full h-full opacity-0 cursor-pointer z-10">
                  
                  <div v-if="!form.programName" class="text-gray-500 group-hover:scale-105 transition-transform duration-300">
                    <i class="bi bi-file-earmark-zip-fill text-[45px] mb-2 block text-emerald-500 drop-shadow-sm"></i>
                    <p class="text-[16px] font-bold text-[#1a1a40]">คลิกเพื่อเลือกไฟล์ ซิป (Zip / Rar)</p>
                    <p class="text-[13px] text-gray-400 mt-1">ขนาดไฟล์ไม่เกิน 100MB</p>
                  </div>
                  
                  <div v-else class="text-green-600 font-bold text-[16px] flex items-center justify-center gap-2 bg-green-50 p-4 rounded-xl border border-green-200 w-full shadow-sm">
                    <i class="bi bi-check-circle-fill text-[24px] shrink-0"></i> 
                    <span class="truncate">{{ form.programName }}</span>
                  </div>
                </div>
              </div>

              <div class="mt-auto">
                <div class="flex items-center gap-4 mb-4">
                  <div class="h-[1.5px] flex-grow bg-gray-100"></div>
                  <span class="text-gray-400 font-medium text-[14px]">หรือ</span>
                  <div class="h-[1.5px] flex-grow bg-gray-100"></div>
                </div>
                
                <label class="block text-[15px] font-medium text-gray-600 mb-3">ระบุลิงก์ดาวน์โหลด / GitHub Repository</label>
                <div class="relative">
                  <div class="absolute inset-y-0 left-0 pl-5 flex items-center pointer-events-none">
                    <i class="bi bi-link-45deg text-gray-400 text-[22px]"></i>
                  </div>
                  <input type="url" v-model="form.programLink" placeholder="https://github.com/..." class="w-full bg-gray-50 border-2 border-gray-200 text-[#1a1a40] text-[15px] rounded-[16px] focus:ring-blue-500 focus:border-blue-500 focus:bg-white block pl-12 p-4 outline-none transition-all shadow-inner">
                </div>
              </div>

            </div>
          </div>

        </div>

        <div class="flex justify-center mt-12 pt-8 border-t-2 border-gray-50">
          <button @click="submitFinalProject" class="w-full md:w-[450px] bg-[#1a1a40] hover:bg-blue-600 hover:-translate-y-1 text-white font-bold py-4 rounded-full transition-all duration-300 flex items-center justify-center gap-3 shadow-[0_8px_20px_rgba(26,26,64,0.2)] hover:shadow-[0_12px_25px_rgba(37,99,235,0.3)] text-[18px]">
            <i class="bi bi-send-fill text-[20px]"></i> ยืนยันการส่งงานฉบับสมบูรณ์
          </button>
        </div>

      </div>

    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

useHead({
  title: 'ส่งเล่มและโปรแกรมฉบับสมบูรณ์'
})

const form = reactive({
  documentName: '',
  programName: '',
  programLink: ''
})

const handleDocumentUpload = (event) => {
  const file = event.target.files[0]
  if (file) {
    form.documentName = file.name
  }
}

const handleProgramUpload = (event) => {
  const file = event.target.files[0]
  if (file) {
    form.programName = file.name
  }
}

const submitFinalProject = () => {
  if (!form.documentName) {
    alert('กรุณาแนบไฟล์รูปเล่ม (PDF) ก่อนครับ')
    return
  }
  if (!form.programName && !form.programLink) {
    alert('กรุณาแนบไฟล์ Source Code หรือ ระบุลิงก์สำหรับดาวน์โหลดโปรแกรมครับ')
    return
  }

  alert('🎉 ส่งงานฉบับสมบูรณ์เรียบร้อยแล้ว! ขอแสดงความยินดีด้วยครับ คุณเรียนจบแล้ว!')
}
</script>