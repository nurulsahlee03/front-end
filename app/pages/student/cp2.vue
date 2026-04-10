<template>
  <div class="min-h-screen bg-gray-100 py-8 px-4 font-['Sarabun',_'Prompt',_sans-serif] print:bg-white print:p-0">
    
    <div class="max-w-[210mm] mx-auto mb-6 flex flex-col md:flex-row justify-between items-center gap-4 print:hidden">
      <NuxtLink to="/student" class="flex items-center gap-2 text-gray-600 hover:text-[#1a1a40] transition-colors font-medium bg-white px-4 py-2 rounded-full shadow-sm w-full md:w-auto justify-center">
        <i class="bi bi-arrow-left"></i> กลับหน้าหลัก
      </NuxtLink>
      
      <div class="flex flex-wrap justify-center gap-2 md:gap-3">
        
        <button @click="saveDraft" class="bg-blue-50 text-blue-600 border border-blue-200 px-4 md:px-6 py-2 rounded-full font-medium hover:bg-blue-100 transition-colors shadow-sm flex items-center gap-2 text-sm md:text-base">
          <i class="bi bi-save"></i> บันทึกข้อมูล
        </button>
        <button @click="printDocument" class="bg-[#1a1a40] text-white px-4 md:px-6 py-2 rounded-full font-medium hover:bg-[#2a2a5c] transition-colors shadow-sm flex items-center gap-2 text-sm md:text-base">
          <i class="bi bi-printer"></i> พิมพ์เอกสาร (CP2)
        </button>
      </div>
    </div>

    <div class="flex flex-col items-center print:block print:w-full print:m-0 print:p-0">
      
      <div class="w-full overflow-x-auto flex justify-center pb-4 print:overflow-visible print:pb-0">
        
        <div class="paper-a4 bg-white shadow-lg relative text-black text-[15px] md:text-[16px] leading-[1.8] print:leading-[1.4] print:shadow-none">
          
          <div class="text-center mb-8 mt-2 print:mb-3 print:mt-0">
            <img src="/bsru_logo.jpg" alt="BSRU Logo" class="w-[80px] mx-auto mb-4 print:mb-1 print:w-[65px]">
            <h2 class="font-bold text-[18px] mb-1 print:text-[16px]">แบบสอบโครงงานคอมพิวเตอร์</h2>
            <h3 class="font-bold text-[16px] print:text-[15px]">สาขาวิชาวิทยาการคอมพิวเตอร์ คณะวิทยาศาสตร์และเทคโนโลยี</h3>
            <h3 class="font-bold text-[16px] print:text-[15px]">มหาวิทยาลัยราชภัฏบ้านสมเด็จเจ้าพระยา</h3>
            <div class="flex justify-center mt-2">
              <div class="border-b-[1.5px] border-dashed border-gray-500 w-[150px]"></div>
            </div>
          </div>

          <div class="flex justify-end mb-6 print:mb-3">
            <div class="flex items-end w-[300px]">
              <span class="whitespace-nowrap">ภาคเรียนที่</span>
              <input type="text" v-model="form.semester" class="form-line w-12 text-center mx-2">
              <span class="whitespace-nowrap">ปีการศึกษา</span>
              <input type="text" v-model="form.academicYear" class="form-line flex-grow text-center ml-2">
            </div>
          </div>

          <div class="mb-8 print:mb-3">
            <div class="flex items-end w-full mb-2 print:mb-1">
              <span class="whitespace-nowrap font-bold">ชื่อเรื่อง (ภาษาไทย)</span>
              <input type="text" v-model="form.projectTitleTh" class="form-line flex-grow ml-2">
            </div>
            <div class="flex items-end w-full">
              <div class="form-line flex-grow h-6 print:h-4 w-full"></div>
            </div>
          </div>

          <div class="mb-6 print:mb-3">
            <div class="font-bold text-center mb-3 print:mb-1">คนที่ 1</div>
            <div class="flex items-end mb-3 print:mb-[2px] w-full">
              <span class="whitespace-nowrap">ชื่อนักศึกษา (นาย/นาง/นางสาว)</span>
              <input type="text" v-model="s1.name" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">รหัสนักศึกษา</span>
              <input type="text" v-model="s1.studentId" class="form-line w-40 ml-2 text-center">
            </div>
            <div class="flex items-end mb-3 print:mb-[2px] w-full">
              <span class="whitespace-nowrap">โทรศัพท์มือถือ</span>
              <input type="text" v-model="s1.phone" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">E-mail</span>
              <input type="email" v-model="s1.email" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">Line Id</span>
              <input type="text" v-model="s1.lineId" class="form-line flex-grow ml-2 text-center">
            </div>
          </div>

          <div class="mb-10 print:mb-4">
            <div class="font-bold text-center mb-3 print:mb-1">คนที่ 2</div>
            <div class="flex items-end mb-3 print:mb-[2px] w-full">
              <span class="whitespace-nowrap">ชื่อนักศึกษา (นาย/นาง/นางสาว)</span>
              <input type="text" v-model="s2.name" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">รหัสนักศึกษา</span>
              <input type="text" v-model="s2.studentId" class="form-line w-40 ml-2 text-center">
            </div>
            <div class="flex items-end mb-3 print:mb-[2px] w-full">
              <span class="whitespace-nowrap">โทรศัพท์มือถือ</span>
              <input type="text" v-model="s2.phone" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">E-mail</span>
              <input type="email" v-model="s2.email" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">Line Id</span>
              <input type="text" v-model="s2.lineId" class="form-line flex-grow ml-2 text-center">
            </div>
          </div>

          <div class="flex justify-between px-10 mb-12 mt-6 print:mt-2 print:mb-4">
            <div class="flex flex-col items-center w-[250px]">
              <div class="flex items-end w-full mb-2 print:mb-1">
                <span class="whitespace-nowrap">ลงชื่อ</span>
                <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                <span class="whitespace-nowrap">นักศึกษา</span>
              </div>
              <div class="flex items-end w-full">
                <span class="whitespace-nowrap">(</span>
                <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 print:h-4 text-center leading-6 print:leading-4 text-gray-600">
                  {{ s1.name }}
                </div>
                <span class="whitespace-nowrap">)</span>
              </div>
            </div>
            <div class="flex flex-col items-center w-[250px]">
              <div class="flex items-end w-full mb-2 print:mb-1">
                <span class="whitespace-nowrap">ลงชื่อ</span>
                <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                <span class="whitespace-nowrap">นักศึกษา</span>
              </div>
              <div class="flex items-end w-full">
                <span class="whitespace-nowrap">(</span>
                <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 print:h-4 text-center leading-6 print:leading-4 text-gray-600">
                  {{ s2.name }}
                </div>
                <span class="whitespace-nowrap">)</span>
              </div>
            </div>
          </div>

          <div class="border-[2px] border-black relative mt-16 print:mt-4 print:break-inside-avoid">
            
            <div class="absolute top-0 right-0 border-l-[2px] border-b-[2px] border-black px-6 py-2 bg-white text-center text-[15px] print:py-1">
              สำหรับอาจารย์ที่ปรึกษา
            </div>
            
            <div class="p-8 pt-12 pb-14 print:p-4 print:pt-8 print:pb-6">
              <div class="mb-8 print:mb-4 font-bold text-[16px]">ความเห็นอาจารย์ที่ปรึกษาโครงงานคอมพิวเตอร์</div>
              
              <div class="flex justify-between items-start px-2">
                <div class="flex flex-col gap-4 print:gap-2 pt-2">
                  <div class="flex items-center gap-3">
                    <span class="whitespace-nowrap">( &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; )</span> 
                    <span>อนุมัติให้สอบได้</span>
                  </div>
                  <div class="flex items-center gap-3">
                    <span class="whitespace-nowrap">( &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; )</span> 
                    <span>ไม่อนุมัติให้สอบ</span>
                  </div>
                </div>

                <div class="flex flex-col items-center w-[400px]">
                  <div class="flex items-end w-full mb-3 print:mb-2">
                    <span class="whitespace-nowrap">ลงชื่อ</span>
                    <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                    <span class="whitespace-nowrap">อาจารย์ที่ปรึกษาหลัก</span>
                  </div>
                  
                  <div class="flex items-end w-full mb-8 print:mb-4">
                    <span class="whitespace-nowrap">(</span>
                    <input type="text" placeholder="พิมพ์ชื่ออาจารย์ที่ปรึกษาหลัก" class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 print:h-4 text-center bg-transparent outline-none text-gray-600 print:placeholder-transparent">
                    <span class="whitespace-nowrap">)</span>
                  </div>

                  <div class="flex items-end w-full pl-6 pr-10">
                    <span class="whitespace-nowrap">วันที่</span>
                    <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4 text-center"></div>
                    <span class="whitespace-nowrap">/</span>
                    <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4 text-center"></div>
                    <span class="whitespace-nowrap">/</span>
                    <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4 text-center"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
        </div>
      </div> </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

useHead({
  title: 'แบบขอสอบจบโครงงาน (CP2)'
})

const form = reactive({
  semester: '',
  academicYear: '',
  projectTitleTh: ''
})

const s1 = reactive({
  name: '', 
  studentId: '',
  phone: '', 
  email: '',
  lineId: ''
})

const s2 = reactive({
  name: '', 
  studentId: '',
  phone: '', 
  email: '',
  lineId: ''
})

const clearForm = () => {
  if (confirm('คุณแน่ใจหรือไม่ว่าต้องการล้างข้อมูลที่กรอกไปแล้วทั้งหมด?')) {
    form.semester = ''
    form.academicYear = ''
    form.projectTitleTh = ''
    s1.phone = ''
    s1.email = ''
    s1.lineId = ''
    s2.name = ''
    s2.studentId = ''
    s2.phone = ''
    s2.email = ''
    s2.lineId = ''
  }
}

const printDocument = () => {
  window.print()
}

const saveDraft = () => {
  alert('บันทึกข้อมูล (ร่าง) CP2 เรียบร้อยแล้ว')
}
</script>

<style>
@media print {
  footer, .footer, header, nav {
    display: none !important;
  }
}
</style>

<style scoped>
.paper-a4 {
  width: 210mm;
  min-height: 297mm;
  padding: 20mm 20mm; 
  box-sizing: border-box;
}

.form-line {
  border: none;
  border-bottom: 1.5px dotted #666;
  background-color: transparent !important;
  outline: none !important;
  box-shadow: none !important;
  font-family: 'Sarabun', sans-serif;
  color: #1a1a40;
  padding: 0 4px;
  margin: 0;
  transition: border-color 0.2s;
}

.form-line:focus {
  border-bottom: 1.5px solid #1a1a40;
}

.border-\[2px\] {
  border-width: 2px !important;
}

@media print {
  @page {
    size: A4 portrait;
    margin: 0mm; 
  }

  html, body {
    margin: 0 !important;
    padding: 0 !important;
    background-color: white !important;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }

  .paper-a4 {
    width: 210mm !important;
    height: 297mm !important; /* บังคับความสูงห้ามเกินนี้เด็ดขาด */
    max-height: 297mm !important;
    margin: 0 !important;
    padding: 12mm 20mm !important; /* ลดขอบกระดาษบน-ล่าง ลงอีกนิด */
    border: none !important;
    box-shadow: none !important;
    box-sizing: border-box !important;
    overflow: hidden !important; /* ป้องกันการล้นไปหน้า 2 */
    page-break-after: avoid !important; /* ห้ามตัดขึ้นหน้าใหม่ */
  }

  .print\:hidden {
    display: none !important;
  }

  .form-line {
    border-bottom: 1px dotted #000 !important;
    color: #000 !important;
  }
  
  .form-line::placeholder {
    color: transparent !important; 
  }
  
  .border-black {
    border-color: black !important;
  }
}
</style>