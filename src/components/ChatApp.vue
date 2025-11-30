<template>
  <div class="min-h-screen chat-bg flex flex-col">
    <div class="flex-1 flex flex-col max-w-xl w-full mx-auto px-4 md:px-10">
      <div
        v-if="!token"
        class="fixed inset-0 z-30 flex items-center justify-center bg-black/40"
      >
        <div
          class="w-full max-w-md bg-white/95 rounded-3xl shadow-2xl p-6 space-y-5"
        >
          <div class="space-y-1 text-center">
            <p class="text-xs font-semibold uppercase text-emerald-700 tracking-wide">
              Rinku Chat · Sign In
            </p>
            <h2 class="text-xl font-bold text-slate-900">
              Masuk dulu, baru curhat ✨
            </h2>
            <p class="text-xs text-slate-500">
              Gunakan akun yang sama dengan backend Subaru Awa-mu.
            </p>
          </div>

          <div class="space-y-3">
            <div class="space-y-1">
              <label class="text-xs font-medium text-slate-700">Username</label>
              <input
                v-model="username"
                type="text"
                class="w-full px-3 py-2 rounded-2xl border text-sm bg-slate-50 focus:bg-white
                       focus:outline-none focus:ring-2 focus:ring-emerald-400"
                placeholder="Masukkan username"
              />
            </div>

            <div class="space-y-1">
              <label class="text-xs font-medium text-slate-700">Password</label>
              <input
                v-model="password"
                type="password"
                class="w-full px-3 py-2 rounded-2xl border text-sm bg-slate-50 focus:bg-white
                       focus:outline-none focus:ring-2 focus:ring-emerald-400"
                placeholder="••••••••"
              />
            </div>

            <p
              v-if="loginError"
              class="text-xs text-red-500 text-center"
            >
              ❌ {{ loginError }}
            </p>

            <button
              @click="handleLogin"
              :disabled="isLoggingIn"
              class="w-full flex items-center justify-center gap-2 py-2.5 mt-1 rounded-2xl text-sm font-semibold
                     text-white bg-emerald-500 hover:bg-emerald-600 active:scale-[0.97]
                     disabled:opacity-70 disabled:cursor-not-allowed"
            >
              <span
                v-if="isLoggingIn"
                class="inline-block w-4 h-4 border-2 border-white border-t-transparent rounded-full animate-spin"
              ></span>
              <span>{{ isLoggingIn ? 'Loading...' : 'Sign In' }}</span>
            </button>
          </div>
        </div>
      </div>

      <ChatHeader
        :active-tab="activeTab"
        @change-tab="activeTab = $event"
      />

      <main class="flex-1 flex flex-col">
        <ChatMessages
          v-if="activeTab === 'Chat'"
          :messages="messages"
        />

        <section
          v-else
          class="flex-1 flex items-center justify-center text-lg font-medium"
        >
          <p v-if="activeTab === 'Beranda'">
            Ini halaman Beranda. Nanti bisa kamu isi apa saja tentang Rinku Chat 💚
          </p>
          <p v-else>
            Di sini kamu bisa menuliskan cerita singkat tentang Rinku ✨
          </p>
        </section>
      </main>

      <ChatInput
        v-if="activeTab === 'Chat'"
        v-model="newMessage"
        :sending="isSending"
        @send="handleSendMessage"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ChatHeader from './ChatHeader.vue'
import ChatMessages from './ChatMessages.vue'
import ChatInput from './ChatInput.vue'

const activeTab = ref('Chat')
const messages = ref([])
const newMessage = ref('')
const isSending = ref(false)

const username = ref('')
const password = ref('')
const loginError = ref('')
const isLoggingIn = ref(false)
const token = ref(null)

const API_BASE_URL = 'https://rinku-api.niaz.my.id'
// const API_BASE_URL = 'http://localhost:3000'
const LOGIN_URL = `${API_BASE_URL}/auth/login`
const CHAT_URL = `${API_BASE_URL}/rinku/chat`

let msgId = 1

function pushMessage(sender, text, extra = {}) {
  messages.value.push({
    id: msgId++,
    sender,
    text,
    ...extra
  })
}

function addTypingIndicator() {
  if (messages.value.some(m => m.type === 'typing')) return
  pushMessage('Rinku', 'typing...', { type: 'typing' })
}

function removeTypingIndicator() {
  messages.value = messages.value.filter(m => m.type !== 'typing')
}

async function handleLogin() {
  loginError.value = ''

  if (!username.value.trim()) {
    loginError.value = 'Username tidak boleh kosong'
    return
  }
  if (!password.value.trim()) {
    loginError.value = 'Password tidak boleh kosong'
    return
  }

  isLoggingIn.value = true
  try {
    const res = await fetch(LOGIN_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        username: username.value.trim(),
        password: password.value.trim()
      })
    })

    const data = await res.json()

    if (res.ok && data.token) {
      token.value = data.token
      if (messages.value.length === 0) {
        pushMessage(
          'Rinku',
          'Hai, aku Aimoto Rinku ✨\n\nKamu bisa curhat atau tanya apa saja di sini.'
        )
      }
    } else {
      loginError.value = data.error || 'Login gagal, cek kembali kredensial kamu.'
    }
  } catch (err) {
    console.error('Login error:', err)
    loginError.value = 'Server tidak bisa diakses. Periksa koneksi atau coba lagi nanti.'
  } finally {
    isLoggingIn.value = false
  }
}

async function handleSendMessage() {
  const text = newMessage.value.trim()
  if (!text) return

  if (!token.value) {
    pushMessage('Rinku', '🔒 Kamu belum login. Silakan login dulu, ya.')
    newMessage.value = ''
    return
  }

  pushMessage('Kamu', text, { type: 'user' })
  newMessage.value = ''
  isSending.value = true

  addTypingIndicator()

  try {
    const res = await fetch(CHAT_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${token.value}`
      },
      body: JSON.stringify({ message: text })
    })

    removeTypingIndicator()

    if (!res.ok) {
      if (res.status === 401 || res.status === 403) {
        pushMessage(
          'Rinku',
          '🔒 Sesi login kamu sudah berakhir. Silakan login ulang ya.'
        )
        token.value = null
        username.value = ''
        password.value = ''
        return
      }
      throw new Error(`Server error: ${res.status}`)
    }

    const data = await res.json()
    const reply = data.reply || 'Tidak ada balasan dari Rinku.'
    pushMessage('Rinku', reply, { type: 'bot' })
  } catch (err) {
    console.error('Chat error:', err)
    removeTypingIndicator()
    pushMessage(
      'Rinku',
      '❌ Maaf, ada masalah saat menghubungi server AI. Coba lagi beberapa saat lagi ya.',
      { type: 'bot' }
    )
  } finally {
    isSending.value = false
  }
}
</script>

<style scoped>
.chat-bg {
  background-color: #e6f7e6;
  background-image:
    linear-gradient(to right, rgba(15, 118, 110, 0.08) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(15, 118, 110, 0.08) 1px, transparent 1px);
  background-size: 40px 40px;
}
</style>
