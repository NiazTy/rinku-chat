<template>
  <section class="flex-1">
    <div class="w-full mt-16 mb-10 pb-40">
      <TransitionGroup
        name="msg"
        tag="div"
        class="space-y-10"
      >
        <div
          v-for="message in messages"
          :key="message.id"
        >
          <div
            v-if="message.sender === 'Kamu'"
            class="flex flex-col items-start"
          >
            <span class="text-xs font-semibold mb-1">
              {{ message.sender }}
            </span>

            <div
              class="px-6 py-3 text-sm leading-relaxed shadow-md
                     max-w-[650px]
                     rounded-full md:rounded-[28px]
                     bg-sky-200 text-slate-900"
            >
              {{ message.text }}
            </div>
          </div>
          <div
            v-else
            class="flex items-end gap-3 justify-end"
          >
            <div class="flex flex-col items-end">
              <span class="text-xs font-semibold mb-1">
                {{ message.sender }}
              </span>
              <div
                v-if="message.type === 'typing'"
                class="px-4 py-2 text-sm shadow-md bg-slate-900 text-white
                       rounded-full md:rounded-[28px] flex items-center gap-1"
              >
                <span class="w-1.5 h-1.5 rounded-full bg-white/70 animate-pulse-slow"></span>
                <span class="w-1.5 h-1.5 rounded-full bg-white/70 animate-pulse-slow delay-150"></span>
                <span class="w-1.5 h-1.5 rounded-full bg-white/70 animate-pulse-slow delay-300"></span>
              </div>

              <div
                v-else
                class="px-6 py-3 text-sm leading-relaxed shadow-md
                       max-w-[650px]
                       rounded-full md:rounded-[28px]
                       bg-slate-900 text-white"
              >
                {{ message.text }}
              </div>
            </div>
            <img
              :src="rinkuAvatar"
              alt="Rinku"
              class="w-10 h-10 md:w-11 md:h-11 rounded-full shadow-md object-cover"
            />
          </div>
        </div>
      </TransitionGroup>

      <div ref="bottomRef" />
    </div>
  </section>
</template>

<script setup>
import { ref, watch, nextTick, defineProps, onMounted } from 'vue'

const props = defineProps({
  messages: {
    type: Array,
    required: true
  }
})

const rinkuAvatar = new URL('../../public/aimoto-rinku.png', import.meta.url).href

const bottomRef = ref(null)

const scrollToBottom = () => {
  if (typeof window === 'undefined') return
  window.scrollTo({
    top: document.documentElement.scrollHeight,
    behavior: 'smooth'
  })
}

onMounted(async () => {
  await nextTick()
  scrollToBottom()
})

watch(
  () => props.messages.length,
  async () => {
    await nextTick()
    scrollToBottom()
  }
)
</script>

<style scoped>
.msg-enter-active {
  transition: all 0.3s ease-out;
}
.msg-enter-from {
  opacity: 0;
  transform: translateY(12px) scale(0.98);
}
.msg-enter-to {
  opacity: 1;
  transform: translateY(0) scale(1);
}

@keyframes pulse-slow {
  0%, 100% { opacity: .3; transform: scale(.8); }
  50% { opacity: 1; transform: scale(1.1); }
}
.animate-pulse-slow {
  animation: pulse-slow 1.5s infinite;
}
</style>
