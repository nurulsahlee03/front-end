<template>
  <div class="p-4 md:p-8 font-['PROMPT',_sans-serif] bg-gray-50 min-h-screen">
    
    <div class="mb-8 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
      <div>
        <h2 class="font-bold text-slate-900 text-2xl md:text-3xl mb-1">ข้อมูลอาจารย์ที่ปรึกษา</h2>
        <p class="text-slate-500 text-sm">รายชื่อและช่องทางการติดต่อของอาจารย์ทั้งหมดในระบบ</p>
      </div>
      
      <button @click="openAddModal" class="bg-[#1a1a40] hover:bg-[#2c2c54] text-white px-6 py-3 rounded-xl text-[15px] font-bold transition-all shadow-lg hover:-translate-y-0.5 flex items-center gap-2 w-fit">
        <i class="bi bi-person-plus-fill text-lg"></i> เพิ่มอาจารย์ใหม่
      </button>
    </div>

    <div class="bg-white rounded-[24px] p-6 shadow-sm border border-slate-100 min-h-[70vh]">
      <div class="flex mb-8">
        <div class="w-full xl:w-[400px] relative">
          <div class="absolute inset-y-0 left-4 flex items-center pointer-events-none text-slate-400">
            <i class="bi bi-search text-lg"></i>
          </div>
          <input 
            type="text" 
            v-model="searchQuery" 
            placeholder="ค้นหาชื่ออาจารย์..." 
            class="w-full bg-slate-50 border border-slate-200 text-slate-700 text-sm rounded-xl pl-11 pr-4 py-3 outline-none focus:border-[#1a1a40] focus:bg-white transition-all"
          >
        </div>
      </div>

      <div class="overflow-x-auto pb-4">
        <table class="w-full text-left border-collapse min-w-[600px]">
          <thead>
            <tr class="border-b-2 border-slate-100 text-slate-400 text-sm">
              <th class="pb-4 font-medium pl-4">ชื่อ - นามสกุล</th>
              <th class="pb-4 font-medium">เบอร์โทรศัพท์</th>
              <th class="pb-4 font-medium">LINE ID</th>
              <th class="pb-4 font-medium text-center">จัดการ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="teacher in filteredTeachers" :key="teacher.id" class="border-b border-slate-50 hover:bg-slate-50 transition-colors">
              <td class="py-4 pl-4 font-bold text-slate-800">{{ teacher.name }}</td>
              <td class="py-4 text-[15px] text-slate-600">{{ teacher.tel }}</td>
              <td class="py-4 text-[15px] text-[#00B900] font-medium">{{ teacher.line }}</td>
              <td class="py-4 text-center">
                <button @click="deleteTeacher(teacher.id, teacher.name)" class="text-rose-400 hover:text-rose-600 p-2 transition-colors">
                  <i class="bi bi-trash text-lg"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      
      <div v-if="filteredTeachers.length === 0" class="py-20 text-center text-slate-400">
        <i class="bi bi-person-badge text-5xl opacity-20"></i>
        <p class="mt-4 font-medium text-slate-500">ไม่พบข้อมูลอาจารย์</p>
      </div>

    </div>

    <div v-if="showAddModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm animate-fade-in">
      <div class="bg-white rounded-[32px] w-full max-w-[750px] shadow-2xl overflow-hidden animate-slide-up">
        
        <div class="px-10 py-6 border-b border-gray-50 flex justify-between items-center">
          <h3 class="font-bold text-[22px] text-[#1a1a40] flex items-center gap-3">
            <div class="w-10 h-10 bg-indigo-50 text-indigo-600 rounded-full flex items-center justify-center">
              <i class="bi bi-person-plus-fill"></i>
            </div>
            เพิ่มอาจารย์ที่ปรึกษา
          </h3>
          <button @click="closeAddModal" class="text-gray-400 hover:text-red-500 transition-colors">
            <i class="bi bi-x-lg text-2xl"></i>
          </button>
        </div>

        <form @submit.prevent="submitAddTeacher" class="p-10 space-y-8">
          
          <div class="space-y-6">
            <div>
              <label class="block font-bold text-slate-700 mb-2.5 text-[16px]">ชื่อ - นามสกุล <span class="text-rose-500">*</span></label>
              <input type="text" v-model="newTeacher.name" required placeholder="เช่น อ. สมชาย ใจดี" class="w-full bg-gray-50 border-2 border-gray-100 rounded-2xl px-5 py-4 text-[16px] focus:border-indigo-500 focus:bg-white outline-none transition-all shadow-inner">
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <label class="block font-bold text-slate-700 mb-2.5 text-[16px]">เบอร์โทรศัพท์</label>
                <input type="text" v-model="newTeacher.tel" placeholder="08X-XXX-XXXX" class="w-full bg-gray-50 border-2 border-gray-100 rounded-2xl px-5 py-4 text-[16px] focus:border-indigo-500 focus:bg-white outline-none transition-all shadow-inner">
              </div>
              <div>
                <label class="block font-bold text-slate-700 mb-2.5 text-[16px]">LINE ID</label>
                <input type="text" v-model="newTeacher.line" placeholder="ID Line" class="w-full bg-gray-50 border-2 border-gray-100 rounded-2xl px-5 py-4 text-[16px] focus:border-indigo-500 focus:bg-white outline-none transition-all shadow-inner">
              </div>
            </div>
          </div>

          <div class="pt-6">
            <button type="submit" class="w-full bg-[#1a1a40] text-white py-5 rounded-[20px] text-[18px] font-bold hover:bg-[#2c2c54] transition-all shadow-xl shadow-indigo-900/20 hover:-translate-y-1 active:scale-[0.98]">
              บันทึกข้อมูลอาจารย์
            </button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

definePageMeta({ layout: 'admin' })

const searchQuery = ref('')
const showAddModal = ref(false)

// เอา username ออกจาก mock data
const teachers = ref([
  { id: 1, name: 'อ. ธีรพัฒน์ ใจดี', tel: '081-234-5678', line: 'teerapat_aj' },
  { id: 2, name: 'ผศ.ดร. สมศรี มีสุข', tel: '089-876-5432', line: 'somsri.m' },
  { id: 3, name: 'อ. มานพ ขยันสอน', tel: '082-333-4444', line: 'manop_cs' },
  { id: 4, name: 'รศ. กานดา รักษาดี', tel: '-', line: '-' }
])

// เอา username ออกจากตัวรับค่า
const newTeacher = reactive({ name: '', tel: '', line: '' })

// ค้นหาเฉพาะชื่อ
const filteredTeachers = computed(() => {
  return teachers.value.filter(t => {
    const search = searchQuery.value.toLowerCase()
    return t.name.toLowerCase().includes(search)
  })
})

const openAddModal = () => {
  Object.keys(newTeacher).forEach(key => newTeacher[key] = '')
  showAddModal.value = true
}

const closeAddModal = () => { showAddModal.value = false }

const submitAddTeacher = () => {
  const newId = teachers.value.length ? Math.max(...teachers.value.map(t => t.id)) + 1 : 1
  teachers.value.push({
    id: newId,
    name: newTeacher.name,
    tel: newTeacher.tel || '-',
    line: newTeacher.line || '-'
  })
  alert(`เพิ่มอาจารย์ "${newTeacher.name}" เรียบร้อยแล้ว`)
  closeAddModal()
}

const deleteTeacher = (id, name) => {
  if (confirm(`ลบข้อมูล "${name}"?`)) {
    teachers.value = teachers.value.filter(t => t.id !== id)
  }
}
</script>

<style scoped>
.animate-fade-in { animation: fadeIn 0.2s ease-out forwards; }
.animate-slide-up { animation: slideUp 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards; }

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(30px) scale(0.98); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}
</style>