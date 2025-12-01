<template>
  <section class="flex-1">
    <div class="w-full mt-24 pb-24">
      <TransitionGroup name="msg" tag="div" class="space-y-6">
        <div v-for="message in messages" :key="message.id" class="px-1">
          <div v-if="message.sender === 'Kamu'" class="flex flex-col items-start gap-1">
            <span class="text-[11px] font-semibold tracking-wide text-emerald-800/80">Kamu</span>
            <div class="max-w-[650px] rounded-3xl md:rounded-[26px] px-5 py-3 text-sm leading-relaxed shadow-lg bg-linear-to-r from-emerald-400 to-emerald-300 text-emerald-950 border border-emerald-200/80">
              {{ message.text }}
            </div>
          </div>
          <div v-else class="flex items-end gap-3 justify-end">
            <!-- Bubble + label -->
            <div class="flex flex-col items-end gap-1">
              <span class="text-[11px] font-semibold tracking-wide text-slate-500/90">{{ message.sender }}</span>
              <!-- Typing indicator -->
              <div v-if="message.type === 'typing'" class="px-4 py-2 text-xs shadow-lg bg-slate-900/95 text-white rounded-2xl md:rounded-[26px] flex items-center gap-1 border border-white/10 backdrop-blur-md">
                <span class="w-1.5 h-1.5 rounded-full bg-white/70 animate-pulse-slow"></span>
                <span class="w-1.5 h-1.5 rounded-full bg-white/70 animate-pulse-slow delay-150"></span>
                <span class="w-1.5 h-1.5 rounded-full bg-white/70 animate-pulse-slow delay-300"></span>
              </div>
              <div v-else class="px-5 py-3 text-sm leading-relaxed shadow-lg rounded-2xl md:rounded-[26px] bg-slate-900/95 text-white prose prose-sm max-w-[650px] prose-invert prose-p:my-1 border border-white/10 backdrop-blur-md" v-html="renderMarkdown(message.text)"></div>
            </div>
            <img :src="dianaAvatar" alt="Rinku" class="w-10 h-10 md:w-11 md:h-11 rounded-full shadow-md object-cover border border-white/70 bg-white" />
          </div>
        </div>
      </TransitionGroup>
      <div ref="bottomRef" />
    </div>
  </section>
</template>

<script setup>
import { ref, watch, nextTick, defineProps, onMounted } from 'vue'
import { marked } from 'marked'

const props = defineProps({
  messages: {
    type: Array,
    required: true
  }
})

const dianaAvatar = new URL('../assets/img/aimoto-rinku/aimoto-rinku.png', import.meta.url).href

marked.setOptions({
  breaks: true
})

function renderMarkdown(text) {
  if (!text) return ''
  return marked.parse(text)
}

const bottomRef = ref(null)

const scrollToBottom = () => {
  if (!bottomRef.value) return
  bottomRef.value.scrollIntoView({ behavior: 'smooth', block: 'end' })
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
  transition: all 0.25s ease-out;
}
.msg-enter-from {
  opacity: 0;
  transform: translateY(10px) scale(0.97);
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