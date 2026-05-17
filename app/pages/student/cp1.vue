<template>
  <div class="min-h-screen bg-[#f3f4f6] py-8 px-4 font-['Sarabun',_sans-serif] text-[16pt] print:bg-white print:py-0 print:px-0 flex flex-col items-center">
    
    <div class="w-full max-w-[210mm] mb-3 print:hidden">
      <NuxtLink to="/student" class="inline-flex items-center gap-2 text-gray-500 hover:text-[#1a1a40] transition-colors font-medium bg-white px-4 py-2 rounded-full shadow-sm text-sm w-fit">
        <i class="bi bi-arrow-left"></i> กลับหน้าหลัก
      </NuxtLink>
    </div>

    <div class="w-full max-w-[210mm] mb-4 print:hidden">
      <div class="bg-white rounded-xl p-3 px-4 md:px-5 shadow-sm border-l-4 flex flex-col md:flex-row justify-between items-start md:items-center gap-3 transition-colors duration-300"
           :class="cp1Status === 'passed' ? 'border-green-500' : (cp1Status === 'scheduled' ? 'border-blue-500' : 'border-gray-300')">
        
        <div class="flex items-start md:items-center gap-3 w-full md:w-auto">
          <div class="p-2 rounded-full shrink-0 mt-1 md:mt-0 transition-colors duration-300"
               :class="cp1Status === 'pending' ? 'bg-gray-100 text-gray-400' : 'bg-blue-50 text-blue-500'">
            <i class="bi bi-calendar-event text-lg"></i>
          </div>
          <div>
            <div class="font-bold text-[#1a1a40] text-[15px]">กำหนดการสอบหัวข้อ (CP1)</div>
            
            <div v-if="cp1Status !== 'pending'" class="text-sm text-gray-500 flex flex-col sm:flex-row sm:items-center sm:gap-2">
              <span><i class="bi bi-clock mr-1"></i> 20 มี.ค. 26 (09:00-10:30 น.)</span>
              <span class="hidden sm:inline">|</span>
              <span><i class="bi bi-geo-alt mr-1"></i> อาคาร 4 ห้อง 412</span>
            </div>
            
            <div v-else class="text-sm text-gray-400 mt-0.5">
              ยังไม่มีกำหนดการสอบ
            </div>
          </div>
        </div>

        <div class="px-3 py-1.5 rounded-full text-sm font-bold flex items-center gap-1.5 shrink-0 self-start md:self-auto transition-colors duration-300"
             :class="cp1Status === 'passed' ? 'bg-green-100 text-green-600' : (cp1Status === 'scheduled' ? 'bg-blue-100 text-blue-600' : 'bg-gray-100 text-gray-500')">
          
          <i v-if="cp1Status === 'passed'" class="bi bi-check-circle-fill"></i>
          <i v-else-if="cp1Status === 'scheduled'" class="bi bi-hourglass-split"></i>
          <i v-else class="bi bi-dash-circle-fill"></i>
          
          {{ cp1Status === 'passed' ? 'ผ่านพิจารณาแล้ว' : (cp1Status === 'scheduled' ? 'รอเข้าสอบ' : 'ยังไม่มีผลพิจารณา') }}
        </div>

      </div>
    </div>

    <div class="w-full max-w-[210mm] mb-6 flex flex-col sm:flex-row justify-between items-center gap-4 print:hidden bg-[#1a1a40] text-white py-3 px-4 md:px-5 rounded-xl shadow-md">
      <div class="font-bold text-[16px] flex items-center gap-2">
        <i class="bi bi-file-earmark-text text-blue-400"></i> แบบขออนุมัติหัวข้อ (CP1)
      </div>
      
      <div class="flex gap-2 w-full sm:w-auto justify-center">
        <button @click="saveDraft" class="flex-1 sm:flex-none justify-center bg-white/10 text-white border border-white/20 px-4 py-1.5 rounded-full font-medium hover:bg-white/20 transition-colors flex items-center gap-2 text-sm">
          <i class="bi bi-save"></i> บันทึกร่าง
        </button>
        <button @click="printDocument" class="flex-1 sm:flex-none justify-center bg-blue-500 text-white px-4 py-1.5 rounded-full font-bold hover:bg-blue-600 transition-colors shadow-sm flex items-center gap-2 text-sm">
          <i class="bi bi-printer"></i> พิมพ์เอกสาร
        </button>
      </div>
    </div>

    <div class="w-full overflow-x-auto pb-16 print:pb-0 print:overflow-visible">
      <div class="flex flex-col items-center gap-8 print:block print:w-full print:gap-0 min-w-[210mm] mx-auto w-[210mm]">
        
        <div class="paper-a4 page-break bg-white shadow-2xl relative text-black text-[16px] leading-relaxed print:shadow-none">
          <div class="text-center mb-5">
            <img src="/bsru_logo.jpg" alt="BSRU Logo" class="w-[80px] mx-auto mb-1 print:w-[70px]">
            <h2 class="font-bold text-[18px]">แบบขออนุมัติหัวข้อโครงงานคอมพิวเตอร์</h2>
            <h3 class="font-bold text-[16px]">สาขาวิชาวิทยาการคอมพิวเตอร์ คณะวิทยาศาสตร์และเทคโนโลยี</h3>
            <h3 class="font-bold text-[16px]">มหาวิทยาลัยราชภัฏบ้านสมเด็จเจ้าพระยา</h3>
          </div>

          <div class="flex items-end justify-end mb-4 gap-2 w-full">
            <span class="shrink-0">ภาคเรียนที่</span>
            <input type="text" v-model="form.semester" class="form-dotted text-center w-12 min-w-0">
            <span class="shrink-0 ml-2">ปีการศึกษา</span>
            <input type="text" v-model="form.academicYear" class="form-dotted text-center w-20 min-w-0">
          </div>

          <div class="flex items-end mb-5 gap-2 w-full">
            <span class="font-bold shrink-0">ชื่อเรื่อง (ภาษาไทย)</span>
            <input type="text" v-model="form.projectTitleTh" class="form-dotted flex-1 min-w-0 font-bold text-blue-800">
          </div>

          <div class="mb-4">
            <div class="font-bold text-center mb-1">คนที่ 1</div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">ชื่อนักศึกษา (นาย/นางสาว)</span>
              <input type="text" v-model="s1.name" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">รหัสนักศึกษา</span>
              <input type="text" v-model="s1.studentId" class="form-dotted w-32 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">ที่อยู่ที่ติดต่อได้ เลขที่</span>
              <input type="text" v-model="s1.addressNo" class="form-dotted w-16 min-w-0 text-center">
              <span class="shrink-0">หมู่ที่</span>
              <input type="text" v-model="s1.moo" class="form-dotted w-12 min-w-0 text-center">
              <span class="shrink-0">ซอย</span>
              <input type="text" v-model="s1.soi" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">ถนน</span>
              <input type="text" v-model="s1.road" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">ตำบล/แขวง</span>
              <input type="text" v-model="s1.subdistrict" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">อำเภอ/เขต</span>
              <input type="text" v-model="s1.district" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">จังหวัด</span>
              <input type="text" v-model="s1.province" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">รหัสไปรษณีย์</span>
              <input type="text" v-model="s1.zipcode" class="form-dotted w-24 min-w-0 text-center">
              <span class="shrink-0">โทรศัพท์มือถือ</span>
              <input type="text" v-model="s1.phone" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">E-mail</span>
              <input type="email" v-model="s1.email" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">Line Id</span>
              <input type="text" v-model="s1.lineId" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">โทรศัพท์บ้าน</span>
              <input type="text" v-model="s1.homePhone" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">กรณีฉุกเฉิน ติดต่อ เบอร์โทร</span>
              <input type="text" v-model="s1.emergencyContact" class="form-dotted flex-1 min-w-0 text-center">
            </div>
          </div>

          <div class="mb-6">
            <div class="font-bold text-center mb-1">คนที่ 2</div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">ชื่อนักศึกษา (นาย/นางสาว)</span>
              <input type="text" v-model="s2.name" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">รหัสนักศึกษา</span>
              <input type="text" v-model="s2.studentId" class="form-dotted w-32 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">ที่อยู่ที่ติดต่อได้ เลขที่</span>
              <input type="text" v-model="s2.addressNo" class="form-dotted w-16 min-w-0 text-center">
              <span class="shrink-0">หมู่ที่</span>
              <input type="text" v-model="s2.moo" class="form-dotted w-12 min-w-0 text-center">
              <span class="shrink-0">ซอย</span>
              <input type="text" v-model="s2.soi" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">ถนน</span>
              <input type="text" v-model="s2.road" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">ตำบล/แขวง</span>
              <input type="text" v-model="s2.subdistrict" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">อำเภอ/เขต</span>
              <input type="text" v-model="s2.district" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">จังหวัด</span>
              <input type="text" v-model="s2.province" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">รหัสไปรษณีย์</span>
              <input type="text" v-model="s2.zipcode" class="form-dotted w-24 min-w-0 text-center">
              <span class="shrink-0">โทรศัพท์มือถือ</span>
              <input type="text" v-model="s2.phone" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">E-mail</span>
              <input type="email" v-model="s2.email" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">Line Id</span>
              <input type="text" v-model="s2.lineId" class="form-dotted flex-1 min-w-0 text-center">
              <span class="shrink-0">โทรศัพท์บ้าน</span>
              <input type="text" v-model="s2.homePhone" class="form-dotted flex-1 min-w-0 text-center">
            </div>
            <div class="flex items-end mb-1.5 gap-2 w-full">
              <span class="shrink-0">กรณีฉุกเฉิน ติดต่อ เบอร์โทร</span>
              <input type="text" v-model="s2.emergencyContact" class="form-dotted flex-1 min-w-0 text-center">
            </div>
          </div>

          <div class="flex justify-between px-8 mb-5 mt-6 w-full break-inside-avoid">
            <div class="flex flex-col items-center w-[250px]">
              <div class="flex items-end gap-2 w-full mb-1">
                <span class="shrink-0">ลงชื่อ</span>
                <input type="text" class="form-dotted flex-1 min-w-0 text-center" readonly>
                <span class="shrink-0">นักศึกษา</span>
              </div>
              <div class="flex items-end gap-1 w-full justify-center">
                <span class="shrink-0">(</span>
                <input type="text" :value="s1.name" class="form-dotted w-[150px] min-w-0 text-center text-gray-700" readonly>
                <span class="shrink-0">)</span>
              </div>
            </div>
            
            <div class="flex flex-col items-center w-[250px]">
              <div class="flex items-end gap-2 w-full mb-1">
                <span class="shrink-0">ลงชื่อ</span>
                <input type="text" class="form-dotted flex-1 min-w-0 text-center" readonly>
                <span class="shrink-0">นักศึกษา</span>
              </div>
              <div class="flex items-end gap-1 w-full justify-center">
                <span class="shrink-0">(</span>
                <input type="text" :value="s2.name" class="form-dotted w-[150px] min-w-0 text-center text-gray-700" readonly>
                <span class="shrink-0">)</span>
              </div>
            </div>
          </div>

          <div class="flex justify-center items-end gap-2 mb-6 w-full break-inside-avoid">
            <span class="shrink-0">วันที่</span>
            <input type="text" value="      /        /      " class="form-dotted w-[180px] min-w-0 text-center text-gray-400" readonly>
          </div>

          <div class="flex justify-between px-4 w-full break-inside-avoid">
            <div class="flex flex-col items-center w-[280px]">
              <div class="flex items-end gap-2 w-full mb-1">
                <span class="shrink-0">ลงชื่อ</span>
                <input type="text" class="form-dotted flex-1 min-w-0 text-center" readonly>
                <span class="shrink-0">ที่ปรึกษาหลัก</span>
              </div>
              <div class="flex items-end gap-1 w-full justify-center">
                <span class="shrink-0">(</span>
                <input type="text" class="form-dotted w-[180px] min-w-0 text-center bg-transparent">
                <span class="shrink-0">)</span>
              </div>
            </div>
            
            <div class="flex flex-col items-center w-[280px]">
              <div class="flex items-end gap-2 w-full mb-1">
                <span class="shrink-0">ลงชื่อ</span>
                <input type="text" class="form-dotted flex-1 min-w-0 text-center" readonly>
                <span class="shrink-0">ที่ปรึกษาร่วม</span>
              </div>
              <div class="flex items-end gap-1 w-full justify-center">
                <span class="shrink-0">(</span>
                <input type="text" class="form-dotted w-[180px] min-w-0 text-center bg-transparent">
                <span class="shrink-0">)</span>
              </div>
            </div>
          </div>

        </div>

        <div class="paper-a4 bg-white shadow-2xl relative text-black text-[16px] leading-relaxed flex flex-col justify-between print:shadow-none print:rounded-none">
          <div>
            <div class="text-right mb-4 text-sm font-bold">CP-1</div>

            <div class="border-[1.5px] border-black p-6 mb-12">
              <h3 class="font-bold text-center mb-6 text-[18px]">ความเห็นของคณะกรรมการสอบหัวข้อโครงงานคอมพิวเตอร์</h3>
              
              <div class="flex flex-col gap-3 mb-6 pl-4">
                <div class="flex items-center gap-4">
                  <div class="w-5 h-5 border-[1.5px] border-black shrink-0"></div>
                  <span>อนุมัติ</span>
                </div>
                <div class="flex items-center gap-4">
                  <div class="w-5 h-5 border-[1.5px] border-black shrink-0"></div>
                  <span>ไม่อนุมัติ</span>
                </div>
              </div>

              <div class="mb-2 pl-4">หมายเหตุเพิ่มเติม</div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 w-full mb-2"></div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 w-full mb-2"></div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 w-full mb-2"></div>
              <div class="border-b-[1.5px] border-dotted border-black h-8 w-full"></div>
            </div>

            <div class="grid grid-cols-2 gap-y-10 px-4 mb-8">
              <div v-for="i in 6" :key="i" class="flex flex-col items-center break-inside-avoid">
                <div class="flex items-end gap-2 w-[250px] mb-1">
                  <span class="shrink-0">ลงชื่อ</span>
                  <input type="text" class="form-dotted flex-1 min-w-0 text-center" readonly>
                  <span class="shrink-0">กรรมการ</span>
                </div>
                <div class="text-center w-[250px] text-gray-500">(........................................................)</div>
              </div>
            </div>
          </div>

          <div class="mt-auto break-inside-avoid">
            <hr class="border-black mb-4 border-[1px]">
            <div class="flex gap-4">
              <span class="font-bold shrink-0">หมายเหตุ</span>
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
import { reactive, ref } from 'vue'

useHead({
  title: 'แบบขออนุมัติหัวข้อโครงงาน (CP1)',
  link: [
    { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=Sarabun:wght@400;700&display=swap' }
  ]
})

// ================= ตัวแปรคุมสถานะการสอบ (เปลี่ยนเพื่อเทส UI ได้เลย) =================
// 'pending' = ยังไม่ยื่น/รอคิว, 'scheduled' = นัดเวลาสอบแล้ว, 'passed' = สอบผ่าน
const cp1Status = ref('pending') 

const form = reactive({ semester: '', academicYear: '', projectTitleTh: '' })
const s1 = reactive({ name: '', studentId: '', addressNo: '', moo: '', soi: '', road: '', subdistrict: '', district: '', province: '', zipcode: '', phone: '', email: '', lineId: '', homePhone: '', emergencyContact: '' })
const s2 = reactive({ name: '', studentId: '', addressNo: '', moo: '', soi: '', road: '', subdistrict: '', district: '', province: '', zipcode: '', phone: '', email: '', lineId: '', homePhone: '', emergencyContact: '' })

const printDocument = () => window.print()
const saveDraft = () => alert('บันทึกข้อมูล (ร่าง) เรียบร้อยแล้ว')
</script>

<style scoped>
/* ================= CSS สำหรับฟอร์ม (หน้าจอ) ================= */
.paper-a4 {
  width: 210mm;
  min-height: 297mm;
  padding: 12mm 15mm; 
  box-sizing: border-box;
  margin: 0 auto;
}

.form-dotted {
  border: none;
  border-bottom: 1.5px dotted #000;
  background-color: transparent !important;
  outline: none !important;
  box-shadow: none !important;
  font-family: 'Sarabun', sans-serif;
  color: #1a1a40;
  border-radius: 0;
  line-height: 1.2;
  padding-bottom: 2px;
}

/* ================= CSS สำหรับสั่ง Print ================= */
@media print {
  @page {
    size: A4 portrait;
    margin: 0cm; 
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
    height: 297mm !important; 
    margin: 0 !important;
    padding: 10mm 15mm !important; 
    border: none !important;
    box-shadow: none !important;
    box-sizing: border-box !important;
    overflow: hidden; 
  }
  
  .page-break {
    page-break-after: always !important;
    break-after: page !important;
  }

  .break-inside-avoid {
    page-break-inside: avoid !important;
    break-inside: avoid !important;
  }

  .print\:hidden {
    display: none !important;
  }

  .form-dotted {
    border-bottom: 1px dotted #000 !important;
    color: #000 !important;
  }
}
</style>