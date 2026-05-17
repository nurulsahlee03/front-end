<template>
  <div class="min-h-screen py-8 px-4 font-['PROMPT'] bg-gray-50">
    <div class="max-w-[900px] mx-auto w-full">
      
      <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-6 gap-4">
        <div class="flex flex-col">
          <NuxtLink 
            to="/student" 
            class="inline-flex items-center gap-2 text-gray-600 hover:text-[#1a1a40] transition-all mb-4 font-medium bg-white px-5 py-2.5 rounded-full shadow-sm border border-gray-200 w-fit text-[15px]"
          >
           <i class="bi bi-arrow-left"></i> กลับหน้าหลัก
          </NuxtLink>
          
          <h2 class="font-bold text-[24px] md:text-[28px] text-[#1a1a40]">
            💻 รายงานความคืบหน้าโปรแกรม
          </h2>
        </div>
        
        <button 
          v-if="latestPercent < 100"
          @click="openAddModal" 
          class="bg-blue-600 text-white px-6 py-2.5 rounded-full font-medium hover:bg-blue-700 transition-all shadow-md flex items-center gap-2"
        >
          <i class="bi bi-plus-lg"></i> เพิ่มรายงาน
        </button>
      </div>

      <div class="relative overflow-hidden rounded-[20px] p-8 text-white shadow-[0_10px_25px_rgba(37,99,235,0.25)] bg-gradient-to-br from-blue-600 to-blue-400 mb-10">
        <i class="bi bi-laptop absolute right-[10%] top-1/2 -translate-y-1/2 text-[8rem] opacity-20 pointer-events-none"></i>
        
        <h4 class="font-bold text-lg mb-1 opacity-90">ความคืบหน้าล่าสุด</h4>
        <div class="text-[3.5rem] font-bold leading-none mb-4">{{ latestPercent }}%</div>
        
        <div class="w-full h-3 bg-white/30 rounded-full overflow-hidden mb-2">
          <div class="h-full bg-white rounded-full transition-all duration-1000 ease-out" :style="{ width: `${latestPercent}%` }"></div>
        </div>
        
        <div class="text-sm opacity-80">Application / System Development</div>
      </div>

      <div class="bg-white rounded-[20px] shadow-[0_4px_25px_rgba(0,0,0,0.05)] p-8 md:p-10">
        <h5 class="font-bold text-[20px] text-[#1a1a40] mb-8 border-b-2 border-gray-100 pb-4">
          ประวัติการรายงาน
        </h5>

        <div v-if="histories.length === 0" class="text-center text-gray-500 py-10">
          <i class="bi bi-inbox text-4xl mb-3 block opacity-50"></i>
          ยังไม่มีข้อมูลรายงานความคืบหน้า
        </div>

        <div v-else class="pl-3">
          <div v-for="(item, index) in histories" :key="item.id" class="relative pl-6 pb-10 last:pb-0">
            <div v-if="index !== histories.length - 1" class="absolute left-[-1px] top-[5px] bottom-[-5px] w-[3px] bg-blue-100 z-0"></div>
            
            <div class="absolute left-[-7px] top-[3px] w-[15px] h-[15px] rounded-full bg-blue-600 border-[3px] border-white shadow-[0_0_0_1px_rgba(37,99,235,1)] z-10"></div>

            <div class="flex flex-col md:flex-row md:items-start justify-between gap-4">
              <div class="w-full">
                <div class="flex justify-between items-center mb-2 w-full">
                  <span class="text-sm text-gray-500 font-medium">
                    <i class="bi bi-clock mr-1"></i> {{ item.date }} น.
                  </span>
                  
                  <div class="flex items-center gap-3">
                    <button @click="openEditModal(item)" class="text-yellow-500 hover:text-yellow-600 transition-colors" title="แก้ไข">
                      <i class="bi bi-pencil-square text-lg"></i>
                    </button>
                    <button @click="deleteHistory(item.id)" class="text-red-400 hover:text-red-600 transition-colors" title="ลบ">
                      <i class="bi bi-trash text-lg"></i>
                    </button>
                  </div>
                </div>

                <div class="bg-gray-50 border border-gray-100 rounded-2xl p-5">
                  <div class="inline-block bg-blue-600 text-white text-xs font-bold px-3 py-1 rounded-full mb-3">
                    System {{ item.percent }}%
                  </div>
                  <p class="text-gray-700 leading-relaxed mb-4 whitespace-pre-wrap">{{ item.detail }}</p>
                  
                  <a v-if="item.file" :href="`/uploads/${item.file}`" target="_blank" class="inline-flex items-center gap-2 bg-white border border-gray-200 text-gray-600 hover:text-blue-600 hover:border-blue-300 px-4 py-2 rounded-full text-sm transition-colors shadow-sm font-medium">
                    <i class="bi bi-file-earmark-text-fill text-blue-500"></i> เปิดดูไฟล์แนบ
                  </a>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>

    </div>

    <div v-if="showAddModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/50 backdrop-blur-sm animate-fade-in">
      <div class="bg-white rounded-[24px] w-full max-w-[700px] shadow-2xl overflow-hidden animate-slide-up">
        
        <div class="px-8 py-5 border-b border-gray-100 flex justify-between items-center bg-gray-50">
          <h3 class="font-bold text-[20px] text-[#1a1a40]">บันทึกผลงาน (โปรแกรม)</h3>
          <button @click="closeAddModal" class="text-gray-400 hover:text-red-500 transition-colors">
            <i class="bi bi-x-lg text-2xl"></i>
          </button>
        </div>

        <form @submit.prevent="submitAdd" class="p-8 space-y-6">
          <div class="bg-blue-50 text-blue-800 text-[15px] p-4 rounded-xl flex items-center gap-2 border border-blue-100">
            <i class="bi bi-info-circle-fill text-lg"></i> ความคืบหน้าล่าสุดของคุณคือ <strong>{{ latestPercent }}%</strong>
          </div>

          <div>
            <label class="block font-bold text-[#1a1a40] mb-2 text-[15px]">ความคืบหน้า (%) <span class="text-red-500">*</span></label>
            <input type="number" v-model="addForm.percent" :min="latestPercent + 1" max="100" required class="w-full border border-gray-300 rounded-xl px-4 py-3 text-lg focus:border-blue-500 focus:ring-1 focus:ring-blue-500 outline-none bg-gray-50 transition-colors">
            <p class="text-sm text-gray-500 mt-2">ต้องมากกว่า {{ latestPercent }}%</p>
          </div>

          <div>
            <label class="block font-bold text-[#1a1a40] mb-2 text-[15px]">รายละเอียดสิ่งที่ทำ <span class="text-red-500">*</span></label>
            <textarea v-model="addForm.detail" rows="5" required placeholder="อธิบายงานที่ทำสำเร็จแล้ว..." class="w-full border border-gray-300 rounded-xl px-4 py-4 text-[15px] focus:border-blue-500 focus:ring-1 focus:ring-blue-500 outline-none bg-gray-50 transition-colors resize-none"></textarea>
          </div>

          <div>
            <label class="block font-bold text-[#1a1a40] mb-2 text-[15px]">ลิงก์งาน / ไฟล์แนบ (ถ้ามี)</label>
            <input type="file" @change="handleAddFile" class="w-full border border-gray-300 rounded-xl px-4 py-3 bg-gray-50 text-[15px] file:mr-4 file:py-2.5 file:px-6 file:rounded-full file:border-0 file:text-sm file:font-bold file:bg-blue-100 file:text-blue-700 hover:file:bg-blue-200 cursor-pointer transition-all">
          </div>

          <div class="pt-6 border-t border-gray-100">
            <button type="submit" class="w-full bg-blue-600 text-white py-4 rounded-xl text-[16px] font-bold hover:bg-blue-700 transition-colors shadow-lg shadow-blue-600/30">
              บันทึกรายงาน
            </button>
          </div>
        </form>
      </div>
    </div>

    <div v-if="showEditModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/50 backdrop-blur-sm animate-fade-in">
      <div class="bg-white rounded-[24px] w-full max-w-[700px] shadow-2xl overflow-hidden animate-slide-up">
        
        <div class="px-8 py-5 border-b border-gray-100 flex justify-between items-center bg-gray-50">
          <h3 class="font-bold text-[20px] text-[#1a1a40]">แก้ไขรายงาน</h3>
          <button @click="closeEditModal" class="text-gray-400 hover:text-red-500 transition-colors">
            <i class="bi bi-x-lg text-2xl"></i>
          </button>
        </div>

        <form @submit.prevent="submitEdit" class="p-8 space-y-6">
          
          <div>
            <label class="block font-bold text-[#1a1a40] mb-2 text-[15px]">ความคืบหน้า (%) <span class="text-red-500">*</span></label>
            <input type="number" v-model="editForm.percent" min="0" max="100" required class="w-full border border-gray-300 rounded-xl px-4 py-3 text-lg focus:border-yellow-500 focus:ring-1 focus:ring-yellow-500 outline-none bg-gray-50 transition-colors">
          </div>

          <div>
            <label class="block font-bold text-[#1a1a40] mb-2 text-[15px]">รายละเอียดสิ่งที่ทำ <span class="text-red-500">*</span></label>
            <textarea v-model="editForm.detail" rows="5" required class="w-full border border-gray-300 rounded-xl px-4 py-4 text-[15px] focus:border-yellow-500 focus:ring-1 focus:ring-yellow-500 outline-none bg-gray-50 transition-colors resize-none"></textarea>
          </div>

          <div>
            <label class="block font-bold text-[#1a1a40] mb-2 text-[15px]">อัพโหลดไฟล์ใหม่ (ถ้าจะเปลี่ยน)</label>
            <input type="file" @change="handleEditFile" class="w-full border border-gray-300 rounded-xl px-4 py-3 bg-gray-50 text-[15px] file:mr-4 file:py-2.5 file:px-6 file:rounded-full file:border-0 file:text-sm file:font-bold file:bg-yellow-100 file:text-yellow-700 hover:file:bg-yellow-200 cursor-pointer transition-all">
            <p class="text-sm text-gray-500 mt-2">* หากไม่เลือก ไฟล์เดิมจะยังอยู่</p>
          </div>

          <div class="pt-6 border-t border-gray-100">
            <button type="submit" class="w-full bg-yellow-500 text-[#1a1a40] py-4 rounded-xl text-[16px] font-bold hover:bg-yellow-400 transition-colors shadow-lg shadow-yellow-500/30">
              บันทึกการแก้ไข
            </button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

useHead({
  title: 'รายงานความคืบหน้าโปรแกรม'
})

// ================= ข้อมูลจำลอง (Mock Data) =================
const histories = ref([
  {
    id: 2,
    percent: 45,
    detail: 'ทำระบบ Login, วางโครงสร้าง Database และหน้า Dashboard ของนักศึกษาเสร็จเรียบร้อยแล้ว',
    date: '18/03/2026 10:30',
    file: 'PROG_1_123456.pdf'
  },
  {
    id: 1,
    percent: 20,
    detail: 'ออกแบบ UI/UX เบื้องต้น และกำหนดขอบเขตของระบบ',
    date: '10/03/2026 14:15',
    file: ''
  }
])

// คำนวณหา % ล่าสุดอัตโนมัติจาก Array
const latestPercent = computed(() => {
  if (histories.value.length === 0) return 0
  // หาค่า percent ที่เยอะที่สุด
  return Math.max(...histories.value.map(item => item.percent))
})

// ================= จัดการ Modal อัพเดทสถานะ =================
const showAddModal = ref(false)
const addForm = reactive({ percent: '', detail: '', file: null })

const openAddModal = () => {
  addForm.percent = latestPercent.value + 10 > 100 ? 100 : latestPercent.value + 10
  addForm.detail = ''
  addForm.file = null
  showAddModal.value = true
}
const closeAddModal = () => { showAddModal.value = false }

const handleAddFile = (e) => { addForm.file = e.target.files[0] }

const submitAdd = () => {
  alert(`บันทึกความคืบหน้า ${addForm.percent}% สำเร็จ!`)
  closeAddModal()
}

// ================= จัดการ Modal แก้ไขสถานะ =================
const showEditModal = ref(false)
const editForm = reactive({ id: null, percent: '', detail: '', file: null })

const openEditModal = (item) => {
  editForm.id = item.id
  editForm.percent = item.percent
  editForm.detail = item.detail
  editForm.file = null
  showEditModal.value = true
}
const closeEditModal = () => { showEditModal.value = false }

const handleEditFile = (e) => { editForm.file = e.target.files[0] }

const submitEdit = () => {
  alert(`อัปเดตข้อมูลความคืบหน้าเรียบร้อยแล้ว!`)
  closeEditModal()
}

// ================= ฟังก์ชันลบรายการ =================
const deleteHistory = (id) => {
  if (confirm('คุณยืนยันที่จะลบรายงานความคืบหน้านี้ใช่หรือไม่?')) {
    alert(`ลบรายการสำเร็จ`)
    // ลบออกจาก Array (จำลอง)
    histories.value = histories.value.filter(h => h.id !== id)
  }
}
</script>

<style scoped>
/* แอนิเมชันสำหรับเปิด-ปิด Modal */
.animate-fade-in {
  animation: fadeIn 0.2s ease-out forwards;
}
.animate-slide-up {
  animation: slideUp 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(20px) scale(0.98); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}
</style>