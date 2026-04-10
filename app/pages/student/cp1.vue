<template>
  <div class="min-h-screen bg-gray-100 py-8 px-4 font-['Sarabun',_'Prompt',_sans-serif] print:bg-white print:p-0">
    
    <div class="max-w-[210mm] mx-auto mb-6 flex flex-col md:flex-row justify-between items-center gap-4 print:hidden">
      <NuxtLink to="/student" class="flex items-center gap-2 text-gray-600 hover:text-[#1a1a40] transition-colors font-medium bg-white px-4 py-2 rounded-full shadow-sm w-full md:w-auto justify-center">
        <i class="bi bi-arrow-left"></i> กลับหน้าหลัก
      </NuxtLink>
      
      <div class="flex flex-wrap justify-center gap-2 md:gap-3">
        
        <button @click="saveDraft" class="bg-blue-50 text-blue-600 border border-blue-200 px-4 md:px-6 py-2 rounded-full font-medium hover:bg-blue-100 transition-colors shadow-sm flex items-center gap-2 text-sm md:text-base">
          <i class="bi bi-save"></i> บันทึก
        </button>
        <button @click="printDocument" class="bg-[#1a1a40] text-white px-4 md:px-6 py-2 rounded-full font-medium hover:bg-[#2a2a5c] transition-colors shadow-sm flex items-center gap-2 text-sm md:text-base">
          <i class="bi bi-printer"></i> พิมพ์เอกสาร
        </button>
      </div>
    </div>

    <div class="flex flex-col items-center gap-8 print:block print:w-full print:gap-0 print:m-0 print:p-0">
      
      <div class="w-full overflow-x-auto flex justify-center pb-4 print:overflow-visible print:pb-0">
        <div class="paper-a4 page-1 bg-white shadow-lg relative text-black text-[15px] md:text-[16px] leading-[1.8] print:leading-[1.5] print:shadow-none">
          
          <div class="text-center mb-8 mt-2 print:mb-4 print:mt-0">
            <img src="/bsru_logo.jpg" alt="BSRU Logo" class="w-[80px] mx-auto mb-4 print:mb-2 print:w-[70px]">
            <h2 class="font-bold text-[18px] mb-1 print:text-[16px]">แบบขออนุมัติหัวข้อโครงงานคอมพิวเตอร์</h2>
            <h3 class="font-bold text-[16px] print:text-[15px]">สาขาวิชาวิทยาการคอมพิวเตอร์ คณะวิทยาศาสตร์และเทคโนโลยี</h3>
            <h3 class="font-bold text-[16px] print:text-[15px]">มหาวิทยาลัยราชภัฏบ้านสมเด็จเจ้าพระยา</h3>
          </div>

          <div class="flex justify-end mb-6 print:mb-4">
            <div class="flex items-end w-[300px]">
              <span class="whitespace-nowrap">ภาคเรียนที่</span>
              <input type="text" v-model="form.semester" class="form-line w-12 text-center mx-2">
              <span class="whitespace-nowrap">ปีการศึกษา</span>
              <input type="text" v-model="form.academicYear" class="form-line flex-grow text-center ml-2">
            </div>
          </div>

          <div class="flex items-end mb-8 print:mb-4">
            <span class="whitespace-nowrap font-bold">ชื่อเรื่อง (ภาษาไทย)</span>
            <input type="text" v-model="form.projectTitleTh" class="form-line flex-grow ml-2">
          </div>

          <div class="mb-8 print:mb-4">
            <div class="font-bold text-center mb-3 print:mb-1">คนที่ 1</div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">ชื่อนักศึกษา (นาย/นางสาว)</span>
              <input type="text" v-model="s1.name" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">รหัสนักศึกษา</span>
              <input type="text" v-model="s1.studentId" class="form-line w-32 ml-2 text-center">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">ที่อยู่ที่ติดต่อได้ เลขที่</span>
              <input type="text" v-model="s1.addressNo" class="form-line w-20 mx-2 text-center">
              <span class="whitespace-nowrap">หมู่ที่</span>
              <input type="text" v-model="s1.moo" class="form-line w-16 mx-2 text-center">
              <span class="whitespace-nowrap">ซอย</span>
              <input type="text" v-model="s1.soi" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">ถนน</span>
              <input type="text" v-model="s1.road" class="form-line flex-grow ml-2">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">ตำบล/แขวง</span>
              <input type="text" v-model="s1.subdistrict" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">อำเภอ/เขต</span>
              <input type="text" v-model="s1.district" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">จังหวัด</span>
              <input type="text" v-model="s1.province" class="form-line flex-grow ml-2">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">รหัสไปรษณีย์</span>
              <input type="text" v-model="s1.zipcode" class="form-line w-24 mx-2 text-center">
              <span class="whitespace-nowrap">โทรศัพท์มือถือ</span>
              <input type="text" v-model="s1.phone" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">E-mail</span>
              <input type="email" v-model="s1.email" class="form-line flex-grow ml-2 text-center">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">Line Id</span>
              <input type="text" v-model="s1.lineId" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">โทรศัพท์บ้าน</span>
              <input type="text" v-model="s1.homePhone" class="form-line flex-grow ml-2 text-center">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">กรณีฉุกเฉิน ติดต่อ เบอร์โทร</span>
              <input type="text" v-model="s1.emergencyContact" class="form-line flex-grow ml-2">
            </div>
          </div>

          <div class="mb-10 print:mb-4">
            <div class="font-bold text-center mb-3 print:mb-1">คนที่ 2</div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">ชื่อนักศึกษา (นาย/นางสาว)</span>
              <input type="text" v-model="s2.name" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">รหัสนักศึกษา</span>
              <input type="text" v-model="s2.studentId" class="form-line w-32 ml-2 text-center">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">ที่อยู่ที่ติดต่อได้ เลขที่</span>
              <input type="text" v-model="s2.addressNo" class="form-line w-20 mx-2 text-center">
              <span class="whitespace-nowrap">หมู่ที่</span>
              <input type="text" v-model="s2.moo" class="form-line w-16 mx-2 text-center">
              <span class="whitespace-nowrap">ซอย</span>
              <input type="text" v-model="s2.soi" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">ถนน</span>
              <input type="text" v-model="s2.road" class="form-line flex-grow ml-2">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">ตำบล/แขวง</span>
              <input type="text" v-model="s2.subdistrict" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">อำเภอ/เขต</span>
              <input type="text" v-model="s2.district" class="form-line flex-grow mx-2">
              <span class="whitespace-nowrap">จังหวัด</span>
              <input type="text" v-model="s2.province" class="form-line flex-grow ml-2">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">รหัสไปรษณีย์</span>
              <input type="text" v-model="s2.zipcode" class="form-line w-24 mx-2 text-center">
              <span class="whitespace-nowrap">โทรศัพท์มือถือ</span>
              <input type="text" v-model="s2.phone" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">E-mail</span>
              <input type="email" v-model="s2.email" class="form-line flex-grow ml-2 text-center">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">Line Id</span>
              <input type="text" v-model="s2.lineId" class="form-line flex-grow mx-2 text-center">
              <span class="whitespace-nowrap">โทรศัพท์บ้าน</span>
              <input type="text" v-model="s2.homePhone" class="form-line flex-grow ml-2 text-center">
            </div>
            
            <div class="flex items-end mb-3 print:mb-[4px] w-full">
              <span class="whitespace-nowrap">กรณีฉุกเฉิน ติดต่อ เบอร์โทร</span>
              <input type="text" v-model="s2.emergencyContact" class="form-line flex-grow ml-2">
            </div>
          </div>

          <div class="print:break-inside-avoid">
            <div class="flex justify-between px-10 mb-8 mt-12 print:mt-4 print:mb-4">
              
              <div class="flex flex-col items-center w-[250px]">
                <div class="flex items-end w-full mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                  <span class="whitespace-nowrap">นักศึกษา</span>
                </div>
                <div class="flex items-end w-full">
                  <span class="whitespace-nowrap">(</span>
                  <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 text-center leading-6 text-gray-600">
                    {{ s1.name }}
                  </div>
                  <span class="whitespace-nowrap">)</span>
                </div>
              </div>

              <div class="flex flex-col items-center w-[250px]">
                <div class="flex items-end w-full mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                  <span class="whitespace-nowrap">นักศึกษา</span>
                </div>
                <div class="flex items-end w-full">
                  <span class="whitespace-nowrap">(</span>
                  <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 text-center leading-6 text-gray-600">
                    {{ s2.name }}
                  </div>
                  <span class="whitespace-nowrap">)</span>
                </div>
              </div>
              
            </div>

            <div class="flex justify-center mb-16 print:mb-6">
              <div class="flex items-end w-[250px]">
                <span class="whitespace-nowrap">วันที่</span>
                <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4 text-center leading-4 text-gray-400">
                   ....../......../......
                </div>
              </div>
            </div>

            <div class="flex justify-between px-4 mb-4 print:mb-0">
              
              <div class="flex flex-col items-center w-[280px]">
                <div class="flex items-end w-full mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                  <span class="whitespace-nowrap">ที่ปรึกษาหลัก</span>
                </div>
                <div class="flex items-end w-full">
                  <span class="whitespace-nowrap">(</span>
                  <input type="text" class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 text-center bg-transparent outline-none text-gray-600 print:placeholder-transparent">
                  <span class="whitespace-nowrap">)</span>
                </div>
              </div>

              <div class="flex flex-col items-center w-[280px]">
                <div class="flex items-end w-full mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-4"></div>
                  <span class="whitespace-nowrap">ที่ปรึกษาร่วม</span>
                </div>
                <div class="flex items-end w-full">
                  <span class="whitespace-nowrap">(</span>
                  <input type="text" class="flex-grow border-b-[1.5px] border-dotted border-black mx-2 h-6 text-center bg-transparent outline-none text-gray-600 print:placeholder-transparent">
                  <span class="whitespace-nowrap">)</span>
                </div>
              </div>

            </div>
          </div>

        </div>
      </div>

      <div class="w-full overflow-x-auto flex justify-center pb-4 print:overflow-visible print:pb-0">
        <div class="paper-a4 page-2 bg-white shadow-lg relative text-black text-[15px] md:text-[16px] leading-[1.8] flex flex-col justify-between print:shadow-none">
          
          <div>
            <div class="text-right mb-6 print:mb-4 text-sm">
              CP-1
            </div>

            <div class="border-[1.5px] border-black p-8 mb-16 print:p-6 print:mb-8">
              <h3 class="font-bold text-center mb-8 print:mb-6 text-[18px]">ความเห็นของคณะกรรมการสอบหัวข้อโครงงานคอมพิวเตอร์</h3>
              
              <div class="flex flex-col gap-6 mb-8 print:mb-6 print:gap-4 pl-4">
                <div class="flex items-center gap-4">
                  <div class="w-6 h-6 border-[1.5px] border-black"></div>
                  <span>อนุมัติ</span>
                </div>
                <div class="flex items-center gap-4">
                  <div class="w-6 h-6 border-[1.5px] border-black"></div>
                  <span>ไม่อนุมัติ</span>
                </div>
              </div>

              <div class="mb-2 pl-4">หมายเหตุเพิ่มเติม</div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 print:h-6 w-full mb-2"></div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 print:h-6 w-full mb-2"></div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 print:h-6 w-full mb-2"></div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 print:h-6 w-full"></div>
            </div>

            <div class="grid grid-cols-2 gap-y-12 print:gap-y-8 px-4 mb-16 print:mb-8">
              
              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>
              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>

              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>
              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>

              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>
              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>

              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>
              <div class="flex flex-col items-center">
                <div class="flex items-end w-full max-w-[280px] justify-center mb-2">
                  <span class="whitespace-nowrap">ลงชื่อ</span>
                  <div class="border-b-[1.5px] border-dotted border-black flex-grow mx-2 h-4"></div>
                  <span class="whitespace-nowrap">กรรมการ</span>
                </div>
                <div class="text-center w-full max-w-[280px]">(...................................................)</div>
              </div>
              
            </div>
          </div>

          <div class="mt-auto">
            <hr class="border-black mb-4 border-[1px]">
            <div class="flex gap-4">
              <span class="font-bold">หมายเหตุ</span>
              <div>
                <p>1. กรุณาแนบบทที่ 1 มาพร้อมกับเอกสารชุดนี้</p>
                <p>2. ให้นำส่งที่ อ.ธีรพัฒน์ ณ ห้อง 412 อาคาร 4 ชั้น 1 สาขาวิชาวิทยาการคอมพิวเตอร์</p>
              </div>
            </div>
          </div>

        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

useHead({
  title: 'แบบขออนุมัติหัวข้อโครงงาน (CP1)',
  link: [
    { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=Sarabun:wght@400;700&display=swap' }
  ]
})

const form = reactive({
  semester: '1',
  academicYear: '2568',
  projectTitleTh: ''
})

const s1 = reactive({
  name: '', 
  studentId: '6611223344',
  addressNo: '', moo: '', soi: '', road: '',
  subdistrict: '', district: '', province: '', zipcode: '',
  phone: '081-234-5678', email: 'example@bsru.ac.th',
  lineId: '', homePhone: '', emergencyContact: ''
})

const s2 = reactive({
  name: '', studentId: '',
  addressNo: '', moo: '', soi: '', road: '',
  subdistrict: '', district: '', province: '', zipcode: '',
  phone: '', email: '',
  lineId: '', homePhone: '', emergencyContact: ''
})

const clearForm = () => {
  if (confirm('คุณแน่ใจหรือไม่ว่าต้องการล้างข้อมูลที่กรอกไปแล้วทั้งหมด?')) {
    form.semester = '1'
    form.academicYear = '2568'
    form.projectTitleTh = ''

    s1.addressNo = ''
    s1.moo = ''
    s1.soi = ''
    s1.road = ''
    s1.subdistrict = ''
    s1.district = ''
    s1.province = ''
    s1.zipcode = ''
    s1.lineId = ''
    s1.homePhone = ''
    s1.emergencyContact = ''

    s2.name = ''
    s2.studentId = ''
    s2.addressNo = ''
    s2.moo = ''
    s2.soi = ''
    s2.road = ''
    s2.subdistrict = ''
    s2.district = ''
    s2.province = ''
    s2.zipcode = ''
    s2.phone = ''
    s2.email = ''
    s2.lineId = ''
    s2.homePhone = ''
    s2.emergencyContact = ''
  }
}

const printDocument = () => {
  window.print()
}

const saveDraft = () => {
  alert('บันทึกข้อมูล (ร่าง) เรียบร้อยแล้ว')
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

/* ================= ปลดล็อคความสูง ให้เบราว์เซอร์จัดการเอง ================= */
@media print {
  @page {
    size: A4 portrait;
    margin: 0; 
  }

  html, body {
    margin: 0 !important;
    padding: 0 !important;
    background-color: white !important;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }

  .paper-a4 {
    width: 100% !important;
    min-height: 0 !important; 
    height: auto !important; 
    margin: 0 !important;
    padding: 10mm 15mm !important; 
    border: none !important;
    box-shadow: none !important;
    box-sizing: border-box !important;
    page-break-inside: avoid !important; 
  }
  
  .page-1 {
    page-break-after: always !important;
    break-after: page !important;
  }
  
  .page-2 {
    page-break-after: auto !important;
    break-after: auto !important;
  }

  .print\:hidden {
    display: none !important;
  }

  .form-line {
    border-bottom: 1px dotted #000 !important;
    color: #000 !important;
  }
}
</style>