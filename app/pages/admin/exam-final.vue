<template>
  <div class="p-4 md:p-8 font-['PROMPT',_sans-serif]">
    
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-8 gap-4">
      <div>
        <h2 class="font-bold text-slate-900 text-2xl md:text-3xl mb-1">คำร้องขอสอบจบ (CP2/CP3)</h2>
        <p class="text-slate-500 text-sm">จัดการคำร้องและบันทึกผลการสอบจบ</p>
      </div>
      
      <div class="flex bg-white rounded-full p-1 shadow-sm border border-slate-100">
        <button @click="activeTab = 'waiting'" 
                :class="activeTab === 'waiting' ? 'bg-[#1a1a40] text-white shadow-md' : 'text-slate-500 hover:bg-slate-50'"
                class="px-6 py-2.5 rounded-full text-sm font-bold transition-all flex items-center gap-2 text-nowrap">
          <i class="bi bi-inbox"></i> รอดำเนินการ
        </button>
        <button @click="activeTab = 'scheduled'" 
                :class="activeTab === 'scheduled' ? 'bg-[#1a1a40] text-white shadow-md' : 'text-slate-500 hover:bg-slate-50'"
                class="px-6 py-2.5 rounded-full text-sm font-bold transition-all flex items-center gap-2 text-nowrap">
          <i class="bi bi-calendar-check"></i> ตารางนัดสอบ
        </button>
      </div>
    </div>

    <div v-if="activeTab === 'waiting'" class="bg-white rounded-[24px] p-6 shadow-sm border border-slate-100 min-h-[500px] animate-[fadeIn_0.3s_ease-in-out]">
      <div class="overflow-x-auto">
        <table class="w-full text-left border-collapse">
          <thead>
            <tr class="border-b-2 border-slate-100 text-slate-400 text-[15px]">
              <th class="pb-4 font-medium px-4">ชื่อโครงงาน</th>
              <th class="pb-4 font-medium">ผู้วิจัย</th>
              <th class="pb-4 font-medium">วันที่ยื่น</th>
              <th class="pb-4 font-medium text-center">เอกสาร (CP2 / CP3)</th>
              <th class="pb-4 font-medium text-center">จัดการ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in waitList" :key="item.id" class="border-b border-slate-50 hover:bg-slate-50 transition-colors">
              <td class="py-4 px-4 font-bold text-slate-800 text-[15px]">{{ item.title }}</td>
              <td class="py-4 text-slate-600">{{ item.student }}</td>
              <td class="py-4 text-slate-500 text-sm">{{ item.date }}</td>
              <td class="py-4">
                <div class="flex items-center justify-center gap-2">
                  <button class="bg-indigo-50 hover:bg-indigo-100 text-indigo-600 px-3 py-1.5 rounded-full text-xs font-bold transition-colors flex items-center gap-1.5 border border-indigo-100">
                    <i class="bi bi-file-earmark-pdf-fill"></i> CP2
                  </button>
                  <button class="bg-rose-50 hover:bg-rose-100 text-rose-600 px-3 py-1.5 rounded-full text-xs font-bold transition-colors flex items-center gap-1.5 border border-rose-100">
                    <i class="bi bi-file-earmark-pdf-fill"></i> CP3
                  </button>
                </div>
              </td>
              <td class="py-4 text-center">
                <button @click="openScheduleModal(item)" class="bg-white border-2 border-[#1a1a40] text-[#1a1a40] hover:bg-[#1a1a40] hover:text-white px-5 py-1.5 rounded-full text-sm font-bold transition-colors">
                  ระบุวันสอบ
                </button>
              </td>
            </tr>
            <tr v-if="waitList.length === 0">
              <td colspan="5" class="py-10 text-center text-slate-400 font-medium">ไม่มีรายการคำร้องขอสอบจบ</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div v-if="activeTab === 'scheduled'" class="bg-white rounded-[24px] p-6 shadow-sm border border-slate-100 min-h-[500px] animate-[fadeIn_0.3s_ease-in-out]">
      <div class="overflow-x-auto">
        <table class="w-full text-left border-collapse">
          <thead>
            <tr class="border-b-2 border-slate-100 text-slate-400 text-[15px]">
              <th class="pb-4 font-medium px-4">วันสอบจบ</th>
              <th class="pb-4 font-medium">เวลา</th>
              <th class="pb-4 font-medium text-center">ห้อง</th>
              <th class="pb-4 font-medium">ผู้วิจัย</th>
              <th class="pb-4 font-medium text-center">จัดการ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in scheduleList" :key="item.id" class="border-b border-slate-50 hover:bg-slate-50 transition-colors">
              <td class="py-4 px-4 font-bold text-rose-600 text-lg">{{ item.examDate }}</td>
              <td class="py-4 font-bold text-slate-700">{{ item.examTime }}</td>
              <td class="py-4 text-center">
                <span class="bg-slate-100 border border-slate-200 text-slate-700 px-3 py-1 rounded-lg text-sm font-bold">{{ item.examRoom }}</span>
              </td>
              <td class="py-4 text-slate-600">{{ item.student }}</td>
              <td class="py-4 text-center">
                <button @click="openResultModal(item)" class="bg-[#1a1a40] hover:bg-emerald-600 text-white px-5 py-1.5 rounded-full text-sm font-bold transition-all shadow-sm flex items-center gap-2 mx-auto">
                  <i class="bi bi-mortarboard"></i> บันทึกผลสอบจบ
                </button>
              </td>
            </tr>
            <tr v-if="scheduleList.length === 0">
              <td colspan="5" class="py-10 text-center text-slate-400 font-medium">ยังไม่มีตารางนัดสอบจบ</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div v-if="showScheduleModal" class="fixed inset-0 z-[100] flex items-center justify-center bg-slate-900/60 backdrop-blur-sm p-4 animate-fade-in">
      <div class="bg-white w-full max-w-[700px] rounded-[32px] p-10 shadow-2xl relative" @click.stop>
        
        <button @click="showScheduleModal = false" class="absolute top-6 right-6 w-10 h-10 flex items-center justify-center rounded-full bg-slate-100 text-slate-400 hover:bg-rose-50 hover:text-rose-500 transition-all">
          <i class="bi bi-x-lg text-xl"></i>
        </button>

        <h3 class="font-bold text-[28px] text-center text-slate-900 mb-10">ระบุวันสอบจบ (CP2/CP3)</h3>
        
        <form @submit.prevent="saveSchedule" class="space-y-6">
          <div class="flex flex-col gap-2">
            <label class="font-bold text-slate-700 text-lg">วันที่</label>
            <input type="date" v-model="scheduleForm.date" required class="w-full bg-white border-2 border-slate-200 text-slate-700 text-lg rounded-2xl px-5 py-4 outline-none focus:border-[#1a1a40] transition-colors cursor-pointer">
          </div>
          
          <div class="flex flex-col gap-2">
            <label class="font-bold text-slate-700 text-lg">เวลา</label>
            <input type="text" v-model="scheduleForm.time" placeholder="เช่น 13:00 - 16:00" required class="w-full bg-white border-2 border-slate-200 text-slate-700 text-lg rounded-2xl px-5 py-4 outline-none focus:border-[#1a1a40] transition-colors">
          </div>
          
          <div class="flex flex-col gap-2">
            <label class="font-bold text-slate-700 text-lg">ห้อง</label>
            <input type="text" v-model="scheduleForm.room" placeholder="เช่น 6125" required class="w-full bg-white border-2 border-slate-200 text-slate-700 text-lg rounded-2xl px-5 py-4 outline-none focus:border-[#1a1a40] transition-colors">
          </div>
          
          <button type="submit" class="w-full bg-[#1a1a40] hover:bg-[#2c2c54] text-white font-bold text-xl py-4 rounded-[20px] mt-8 shadow-xl flex justify-center items-center gap-3 transition-transform hover:-translate-y-1">
            <i class="bi bi-plus-circle-fill"></i> บันทึกตารางสอบจบ
          </button>
        </form>
      </div>
    </div>

    <div v-if="showResultModal" class="fixed inset-0 z-[101] flex items-center justify-center bg-slate-900/60 backdrop-blur-sm p-4 animate-fade-in">
      <div class="bg-white w-full max-w-[850px] rounded-[32px] p-8 md:p-12 shadow-2xl relative" @click.stop>
        
        <button @click="showResultModal = false" class="absolute top-6 right-6 w-10 h-10 flex items-center justify-center rounded-full bg-slate-100 text-slate-400 hover:bg-slate-200 hover:text-rose-600 transition-all">
          <i class="bi bi-x-lg text-xl"></i>
        </button>

        <div class="text-center mb-10">
          <h3 class="font-bold text-3xl text-slate-900">บันทึกผลการสอบจบ (CP3)</h3>
          <p class="text-slate-500 mt-2">ยืนยันผลการพิจารณาสอบจบและให้เกรดโครงงาน</p>
        </div>

        <form @submit.prevent="saveResult" class="space-y-8">
          
          <div class="flex flex-col gap-3">
            <label class="font-bold text-slate-700 text-lg">ผลการพิจารณา</label>
            <div class="flex gap-4 w-full">
              <label class="flex-1 cursor-pointer group">
                <input type="radio" v-model="resultForm.status" value="pass" class="hidden peer">
                <div class="px-6 py-4 rounded-2xl border-2 border-slate-100 hover:border-emerald-300 hover:bg-emerald-50/30 peer-checked:border-emerald-500 peer-checked:bg-emerald-50 text-slate-400 peer-checked:text-emerald-600 font-bold transition-all text-center text-lg flex items-center justify-center gap-2">
                  <i class="bi bi-check-circle-fill text-xl"></i> ผ่าน
                </div>
              </label>
              <label class="flex-1 cursor-pointer group">
                <input type="radio" v-model="resultForm.status" value="fail" class="hidden peer">
                <div class="px-6 py-4 rounded-2xl border-2 border-slate-100 hover:border-rose-300 hover:bg-rose-50/30 peer-checked:border-rose-500 peer-checked:bg-rose-50 text-slate-400 peer-checked:text-rose-600 font-bold transition-all text-center text-lg flex items-center justify-center gap-2">
                  <i class="bi bi-x-circle-fill text-xl"></i> ไม่ผ่าน / แก้ไขเล่ม
                </div>
              </label>
            </div>
          </div>

          <div v-if="resultForm.status === 'pass'" class="flex flex-col gap-2 animate-fade-in">
            <label class="font-bold text-slate-700 text-lg">ให้เกรด</label>
            <div class="relative">
              <select v-model="resultForm.grade" class="w-full bg-slate-50 border-2 border-slate-200 rounded-2xl px-5 py-4 text-lg font-bold outline-none focus:border-[#1a1a40] focus:bg-white appearance-none cursor-pointer transition-all">
                <option value="A">Grade A</option>
                <option value="B+">Grade B+</option>
                <option value="B">Grade B</option>
                <option value="C+">Grade C+</option>
                <option value="C">Grade C</option>
                <option value="D+">Grade D+</option>
                <option value="D">Grade D</option>
              </select>
              <div class="absolute inset-y-0 right-5 flex items-center pointer-events-none text-slate-400">
                <i class="bi bi-chevron-down font-bold text-lg"></i>
              </div>
            </div>
          </div>

          <div class="flex flex-col gap-2">
            <label class="font-bold text-slate-700 text-lg">รายละเอียดการพิจารณา / ข้อเสนอแนะเพิ่มเติม</label>
            <textarea v-model="resultForm.details" rows="6" placeholder="กรอกข้อเสนอแนะสำหรับการแก้ไขเล่ม หรือระบุสาเหตุที่ไม่ผ่านอย่างละเอียด..." class="w-full bg-slate-50 border-2 border-slate-200 rounded-2xl px-6 py-5 outline-none focus:bg-white focus:border-[#1a1a40] transition-all text-base text-slate-700 resize-none shadow-inner"></textarea>
          </div>

          <div class="flex gap-4 pt-4">
            <button @click="showResultModal = false" type="button" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-600 font-bold py-4 rounded-2xl transition-all text-lg">
              ยกเลิก
            </button>
            <button type="submit" class="flex-[2] bg-[#1a1a40] hover:bg-[#2c2c54] text-white font-bold text-lg py-4 rounded-2xl shadow-xl flex justify-center items-center gap-2 transition-transform hover:-translate-y-1 active:scale-95">
              <i class="bi bi-cloud-arrow-up-fill"></i> ยืนยันบันทึกผลสอบจบ
            </button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

definePageMeta({ layout: 'admin' })

const activeTab = ref('waiting')
const showScheduleModal = ref(false)
const showResultModal = ref(false)

const scheduleForm = ref({ projectId: null, date: '', time: '', room: '' })
const resultForm = ref({ projectId: null, status: 'pass', grade: 'A', details: '' })

const waitList = ref([
  { id: 4, title: 'เกมส่งเสริมการเรียนรู้คำศัพท์ภาษาอังกฤษแบบ AR', student: 'นางสาวรักเรียน เพียรศึกษา', date: '20/08/2026' }
])

const scheduleList = ref([
  { id: 5, title: 'ระบบ IoT ตรวจวัดคุณภาพดินอัจฉริยะ', student: 'นายเก่ง กล้าหาญ', examDate: '01/09/2026', examTime: '10:00 - 12:00', examRoom: 'IT-502' }
])

const openScheduleModal = (item) => {
  scheduleForm.value.projectId = item.id
  scheduleForm.value.date = ''
  scheduleForm.value.time = ''
  scheduleForm.value.room = ''
  showScheduleModal.value = true
}

const openResultModal = (item) => {
  resultForm.value.projectId = item.id
  resultForm.value.status = 'pass'
  resultForm.value.grade = 'A'
  resultForm.value.details = ''
  showResultModal.value = true
}

const saveSchedule = () => {
  alert('จัดตารางสอบจบเรียบร้อยแล้ว!')
  showScheduleModal.value = false
}

const saveResult = () => {
  const text = resultForm.value.status === 'pass' ? `ผ่าน (เกรด ${resultForm.value.grade})` : 'ไม่ผ่าน'
  alert(`บันทึกผลสอบจบสำเร็จ: ${text}\nรายละเอียด: ${resultForm.value.details}`)
  showResultModal.value = false
}
</script>

<style>
.animate-fade-in { animation: fadeIn 0.2s ease-out forwards; }

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>