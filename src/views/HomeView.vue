<template>
  <div class="relative min-h-screen overflow-hidden bg-green-50">
    <!-- GRID BACKGROUND -->
    <div class="absolute inset-0 bg-[linear-gradient(#b7e4c7_1px,transparent_1px),linear-gradient(90deg,#b7e4c7_1px,transparent_1px)] bg-size-[24px_24px] opacity-40"></div>
    <!-- BASE BACKGROUND -->
    <div class="absolute inset-0 bg-green-50"></div>
    <!-- GRADIENT BLUR KIRI -->
    <div class="absolute -left-40 top-1/4 w-[600px] h-[600px]
                bg-green-300/40 rounded-full blur-[120px]"></div>
    <!-- GRADIENT BLUR KANAN -->
    <div class="absolute -right-40 top-1/3 w-[600px] h-[600px]
                bg-green-300/40 rounded-full blur-[120px]"></div>
    <!-- GRID BACKGROUND -->
    <div class="absolute inset-0 bg-[linear-gradient(#b7e4c7_1px,transparent_1px), linear-gradient(90deg,#b7e4c7_1px,transparent_1px)] bg-size-[24px_24px] opacity-40"></div>
    
    <Navbar />

    <main class="relative z-10 flex flex-col items-center justify-center min-h-screen px-6">

      <!-- Chat bubbles -->
      <div class="absolute left-10 top-1/2 -translate-y-1/2 hidden lg:block">
        <ChatBubble
          text="Kamu gagal? Aman, selama kamu masih bisa membaca kamu berhasil!"
          position="left"
        />
      </div>

      <div class="absolute right-10 top-1/2 -translate-y-1/2 hidden lg:block">
        <ChatBubble
          text="Nggak apa-apa jatuh, yang penting kamu nggak berhenti."
          position="right"
        />
      </div>

      <!-- Character -->
      <div class="relative flex flex-col items-center">
        <div class="absolute w-[420px] h-[420px] rounded-full border-4 border-green-300 opacity-40"></div>

        <img
          src="@/assets/img/aimoto-rinku/aimoto-rinku.png"
          alt="Rinku"
          class="w-[260px] relative z-10"
        />

        <h1 class="mt-6 text-5xl font-extrabold text-green-300 tracking-wide drop-shadow">
          NAMAKU RINKU
        </h1>
      </div>

      <!-- Input -->
      <div class="mt-10 flex items-center bg-green-200 px-6 py-4 rounded-full w-full max-w-md shadow-lg">
        <input
          type="text"
          placeholder="Siapa Nama Kamu?"
          class="flex-1 bg-transparent outline-none text-green-900 placeholder-green-700"
        />
        <button class="ml-4 text-green-700 hover:scale-110 transition">
          ➤
        </button>
      </div>

    </main>
  </div>
</template>

<script setup>
import Navbar from '@/components/Navbar.vue'
import ChatBubble from '@/components/ChatBubble.vue'
</script>
