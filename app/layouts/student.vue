<template>
  <div class="flex flex-col min-h-screen bg-[#f8f9fa] font-['PROMPT',_sans-serif]">
    <nav
      class="sticky top-0 z-40 bg-[#252243] py-3 shadow-[0_4px_20px_rgba(0,0,0,0.1)] print:hidden"
    >
      <div
        class="w-full max-w-7xl mx-auto px-4 md:px-8 flex items-center justify-between"
      >
        <NuxtLink
          to="/student"
          class="text-white font-bold text-[1.4rem] flex items-center gap-2 no-underline shrink-0"
        >
          <i class="bi bi-mortarboard-fill text-[#ffc107]"></i> Student Panel
        </NuxtLink>

        <button
          @click="isMenuOpen = true"
          class="lg:hidden text-white text-2xl focus:outline-none transition-transform active:scale-95"
        >
          <i class="bi bi-list"></i>
        </button>

        <div class="hidden lg:flex items-center gap-6">
          <ul class="flex items-center gap-2 m-0 p-0 list-none">
            <li>
              <NuxtLink
                to="/procedures"
                active-class="bg-white/20 text-white font-bold"
                class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-4 py-2 rounded-full transition-all text-[0.95rem]"
              >
                <i class="bi bi-diagram-3-fill"></i> กระบวนการจัดทำโครงงาน
              </NuxtLink>
            </li>
            <li>
              <NuxtLink
                to="/student"
                active-class="bg-white/20 text-white font-bold"
                class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-4 py-2 rounded-full transition-all text-[0.95rem]"
              >
                <i class="bi bi-folder-fill"></i> จัดการโครงงาน
              </NuxtLink>
            </li>
            <li>
              <NuxtLink
                to="/senior-projects"
                active-class="bg-white/20 text-white font-bold"
                class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-4 py-2 rounded-full transition-all text-[0.95rem]"
              >
                <i class="bi bi-collection-play-fill"></i> ฐานข้อมูลบัณฑิตนิพนธ์
              </NuxtLink>
            </li>
            <li>
              <a
                href="/thesis_manual.pdf"
                target="_blank"
                class="flex items-center gap-2 text-white/80 hover:text-white hover:bg-white/10 px-4 py-2 rounded-full transition-all text-[0.95rem]"
              >
                <i class="bi bi-book-half"></i> คู่มือจัดทำบัณฑิตนิพนธ์
              </a>
            </li>
          </ul>

          <div class="w-px h-6 bg-white/20"></div>
          <div class="flex items-center gap-3">
            <NuxtLink
              to="/student/profile"
              class="flex items-center gap-[10px] text-white bg-white/10 hover:bg-white/20 transition-colors duration-300 pr-4 pl-1.5 py-1.5 rounded-full no-underline"
            >
              <div
                class="w-[28px] h-[28px] bg-white text-[#1a1a40] rounded-full flex items-center justify-center font-bold text-xs"
              >
                น
              </div>
              <span class="text-[0.9rem] font-medium">นางสาวตัวอย่าง ใจดี</span>
            </NuxtLink>
            <button
              @click="handleLogout"
              class="flex items-center justify-center w-9 h-9 text-white border border-white/30 hover:bg-rose-500 hover:border-rose-500 rounded-full transition-colors duration-300"
              title="ออกจากระบบ"
            >
              <i class="bi bi-box-arrow-right"></i>
            </button>
          </div>
        </div>
      </div>
    </nav>

    <aside
      :class="isMenuOpen ? 'translate-x-0' : '-translate-x-full'"
      class="fixed top-0 left-0 z-[100] w-[280px] h-[100dvh] bg-[#252243] shadow-2xl transition-transform duration-300 ease-in-out lg:hidden flex flex-col print:hidden"
    >
      <div class="p-5 flex items-center justify-between border-b border-white/10">
        <div class="text-white font-bold text-lg flex items-center gap-2">
          <i class="bi bi-mortarboard-fill text-[#ffc107]"></i> Menu
        </div>
        <button
          @click="isMenuOpen = false"
          class="text-white/70 hover:text-white text-2xl transition-colors focus:outline-none"
        >
          <i class="bi bi-x-lg"></i>
        </button>
      </div>

      <div class="p-4 border-b border-white/10 bg-white/5 flex items-center gap-3">
        <div
          class="w-12 h-12 bg-white text-[#1a1a40] rounded-full flex items-center justify-center font-bold text-lg shrink-0"
        >
          น
        </div>
        <div class="text-white overflow-hidden">
          <div class="font-medium text-sm truncate">นางสาวตัวอย่าง ใจดี</div>
          <div class="text-xs text-[#ffc107] mt-0.5">6611223344</div>
        </div>
      </div>

      <nav class="flex-grow p-4 space-y-2 overflow-y-auto">
        <NuxtLink
          to="/student"
          @click="closeMenu"
          exact-active-class="bg-white/20 text-white font-bold border-l-4 border-[#ffc107]"
          class="flex items-center gap-3 text-white/80 hover:text-white hover:bg-white/10 px-4 py-3 rounded-r-xl transition-all"
        >
          <i class="bi bi-folder-fill"></i> จัดการโครงงาน
        </NuxtLink>
        <NuxtLink
          to="/procedures"
          @click="closeMenu"
          active-class="bg-white/20 text-white font-bold border-l-4 border-[#ffc107]"
          class="flex items-center gap-3 text-white/80 hover:text-white hover:bg-white/10 px-4 py-3 rounded-r-xl transition-all"
        >
          <i class="bi bi-diagram-3-fill"></i> กระบวนการจัดทำโครงงาน
        </NuxtLink>
        <NuxtLink
          to="/senior-projects"
          @click="closeMenu"
          active-class="bg-white/20 text-white font-bold border-l-4 border-[#ffc107]"
          class="flex items-center gap-3 text-white/80 hover:text-white hover:bg-white/10 px-4 py-3 rounded-r-xl transition-all"
        >
          <i class="bi bi-collection-play-fill"></i> ฐานข้อมูลบัณฑิตนิพนธ์
        </NuxtLink>
        <a
          href="/thesis_manual.pdf"
          target="_blank"
          @click="closeMenu"
          class="flex items-center gap-3 text-white/80 hover:text-white hover:bg-white/10 px-4 py-3 rounded-r-xl transition-all"
        >
          <i class="bi bi-book-half"></i> คู่มือจัดทำบัณฑิตนิพนธ์
        </a>
      </nav>

      <div class="p-4 mt-auto border-t border-white/10">
        <button
          @click="handleLogout"
          class="w-full flex items-center justify-center gap-2 text-white bg-rose-500 hover:bg-rose-600 px-4 py-3.5 rounded-xl text-sm font-bold transition-colors"
        >
          <i class="bi bi-box-arrow-right text-lg"></i> ออกจากระบบ
        </button>
      </div>
    </aside>

    <div
      v-if="isMenuOpen"
      @click="isMenuOpen = false"
      class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-[90] lg:hidden transition-opacity print:hidden"
    ></div>

    <main class="flex-grow w-full max-w-7xl mx-auto py-6 px-4 md:px-8">
      <slot />
    </main>

    <footer class="bg-[#1a1a40] text-white mt-auto print:hidden">
      <div class="bg-black/20 text-center p-4 text-sm mt-10">
        © 2026 Copyright: <span class="text-[#ffc107]">BSRU Computer Science</span>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const isMenuOpen = ref(false);

const closeMenu = () => {
  isMenuOpen.value = false;
};

const handleLogout = () => {
  if (confirm("คุณต้องการออกจากระบบใช่หรือไม่?")) {
    router.push("/login");
  }
};

useHead({
  titleTemplate: "%s | BSRU Computer Project",
  link: [
    {
      rel: "stylesheet",
      href:
        "https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap",
    },
    {
      rel: "stylesheet",
      href:
        "https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css",
    },
  ],
});
</script>
