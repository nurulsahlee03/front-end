<template>
  <div class="flex flex-col lg:flex-row min-h-screen bg-[#f0f2f5] font-['PROMPT']">
    
    <div class="lg:hidden bg-gradient-to-r from-[#0f0c29] to-[#302b63] text-white p-4 flex justify-between items-center sticky top-0 z-50 shadow-md print:hidden">
      <div class="flex items-center gap-3">
        <div class="w-8 h-8 rounded-full bg-white text-[#0f0c29] flex items-center justify-center font-bold text-sm shadow-inner shrink-0">
          A
        </div>
        <span class="font-bold text-[15px]">Admin System</span>
      </div>
      <button @click="isMobileMenuOpen = !isMobileMenuOpen" class="text-white text-2xl focus:outline-none transition-transform active:scale-95">
        <i :class="isMobileMenuOpen ? 'bi bi-x-lg' : 'bi bi-list'"></i>
      </button>
    </div>

    <aside :class="isMobileMenuOpen ? 'translate-x-0' : '-translate-x-full lg:translate-x-0'" class="w-[260px] bg-gradient-to-b from-[#0f0c29] to-[#302b63] text-white flex flex-col shadow-[4px_0_15px_rgba(0,0,0,0.1)] shrink-0 fixed lg:sticky top-0 h-screen transition-transform duration-300 ease-in-out z-40 print:hidden">
      
      <div class="p-8 border-b border-white/10 flex items-center gap-4">
        <div class="w-12 h-12 rounded-full bg-white text-[#0f0c29] flex items-center justify-center font-bold text-xl shadow-inner shrink-0">
          A
        </div>
        <div class="overflow-hidden">
          <span class="block font-bold truncate text-[15px]">Admin System</span>
          <span class="text-white/50 text-xs">Administrator</span>
        </div>
      </div>

      <nav class="flex-grow p-4 space-y-2 overflow-y-auto">
        <NuxtLink to="/admin" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-grid-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">Dashboard</span>
        </NuxtLink>

        <NuxtLink to="/admin/exam-topic" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-clipboard-check-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">คำร้องขอสอบหัวข้อ</span>
        </NuxtLink>

        <NuxtLink to="/admin/exam-final" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-clipboard-data-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">คำร้องขอสอบจบ</span>
        </NuxtLink>

        <NuxtLink to="/admin/projects" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-folder-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">ข้อมูลโครงงาน</span>
        </NuxtLink>

        <NuxtLink to="/admin/students/students" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-people-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">ข้อมูลนักศึกษา</span>
        </NuxtLink>

        <NuxtLink to="/admin/teachers" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-person-badge-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">ข้อมูลอาจารย์</span>
        </NuxtLink>

        <NuxtLink to="/admin/reports" @click="closeMenu" exact-active-class="bg-white !text-[#0f0c29] font-bold shadow-lg" class="flex items-center gap-3 text-[#b8c6db] hover:text-white hover:bg-white/10 px-4 py-3 rounded-xl transition-all duration-300 group">
          <i class="bi bi-file-earmark-bar-graph-fill text-lg w-6 text-center group-hover:scale-110 transition-transform"></i>
          <span class="text-sm">รายงาน</span>
        </NuxtLink>
      </nav>

      <div class="p-4 mt-auto">
        <button @click="handleLogout" class="w-full flex items-center justify-center gap-2 bg-[#e0e0e0] hover:bg-white text-slate-800 hover:text-rose-600 font-bold px-4 py-3.5 rounded-xl transition-colors duration-300 shadow-sm">
          <i class="bi bi-box-arrow-right text-lg"></i> ออกจากระบบ
        </button>
      </div>
    </aside>

    <div v-if="isMobileMenuOpen" @click="closeMenu" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-30 lg:hidden transition-opacity print:hidden"></div>

    <main class="flex-grow w-full max-w-full overflow-x-hidden p-0 md:p-2">
      <slot />
    </main>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const isMobileMenuOpen = ref(false);

const closeMenu = () => {
  isMobileMenuOpen.value = false;
};

const handleLogout = () => {
  if (confirm("คุณต้องการออกจากระบบ Admin ใช่หรือไม่?")) {
    router.push("/login");
  }
};

useHead({
  link: [
    { rel: "stylesheet", href: "https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap" },
    { rel: "stylesheet", href: "https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css" }
  ]
});
</script>