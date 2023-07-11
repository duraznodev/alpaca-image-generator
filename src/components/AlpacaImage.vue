<script setup>
import { ref } from 'vue'

defineProps({
  alpaca: Object
})

console.log()
const img = ref(null)

function handleDownload() {
  const canvas = document.createElement('canvas')
  canvas.width = img.value.offsetWidth
  canvas.height = img.value.offsetHeight
  const imgs = img.value.querySelectorAll('img')
  const ctx = canvas.getContext('2d')

  imgs.forEach((img) => {
    ctx.drawImage(img, 0, 0, canvas.width, canvas.height)
  })

  const link = document.createElement('a')
  link.href = canvas.toDataURL('img/png')
  link.download = 'alpaca.png'

  link.click()
}
</script>
<template>
  <div>
    <div ref="img" class="relative aspect-square w-96 bg-blue-950">
      <img
        class="absolute"
        :src="`/public/alpaca/backgrounds/${alpaca.background}.png`"
        alt="alpaca background"
      />
      <img class="absolute" :src="`/public/alpaca/ears/${alpaca.ears}.png`" alt="alpaca ears" />
      <img class="absolute" :src="`/public/alpaca/neck/${alpaca.neck}.png`" alt="alpaca neck" />
      <img class="absolute" :src="`/public/alpaca/hair/${alpaca.hair}.png`" alt="alpaca hair" />
      <img class="absolute" :src="`/public/alpaca/eyes/${alpaca.eyes}.png`" alt="alpaca eyes" />
      <img class="absolute" :src="`/public/alpaca/leg/${alpaca.leg}.png`" alt="alpaca leg" />
      <img
        v-if="alpaca.accesories"
        class="absolute"
        :src="`/public/alpaca/accessories/${alpaca.accesories}.png`"
        alt="alpaca accesories"
      />
      <img class="absolute" src="/public/alpaca/nose.png" alt="alpaca nose" />
      <img class="absolute" :src="`/public/alpaca/mouth/${alpaca.mouth}.png`" alt="alpaca mouth" />
    </div>
    <div class="mt-4 flex gap-x-4">
      <button
        @click="$emit('randomAlpaca', 'random')"
        class="flex flex-1 items-center justify-center gap-x-2 rounded bg-white py-4 text-xl font-semibold tracking-wide shadow"
      >
        <svg
          class="opacity-80"
          xmlns="http://www.w3.org/2000/svg"
          height="1em"
          viewBox="0 0 512 512"
        >
          <path
            d="M403.8 34.4c12-5 25.7-2.2 34.9 6.9l64 64c6 6 9.4 14.1 9.4 22.6s-3.4 16.6-9.4 22.6l-64 64c-9.2 9.2-22.9 11.9-34.9 6.9s-19.8-16.6-19.8-29.6V160H352c-10.1 0-19.6 4.7-25.6 12.8L284 229.3 244 176l31.2-41.6C293.3 110.2 321.8 96 352 96h32V64c0-12.9 7.8-24.6 19.8-29.6zM164 282.7L204 336l-31.2 41.6C154.7 401.8 126.2 416 96 416H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H96c10.1 0 19.6-4.7 25.6-12.8L164 282.7zm274.6 188c-9.2 9.2-22.9 11.9-34.9 6.9s-19.8-16.6-19.8-29.6V416H352c-30.2 0-58.7-14.2-76.8-38.4L121.6 172.8c-6-8.1-15.5-12.8-25.6-12.8H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H96c30.2 0 58.7 14.2 76.8 38.4L326.4 339.2c6 8.1 15.5 12.8 25.6 12.8h32V320c0-12.9 7.8-24.6 19.8-29.6s25.7-2.2 34.9 6.9l64 64c6 6 9.4 14.1 9.4 22.6s-3.4 16.6-9.4 22.6l-64 64z"
          />
        </svg>
        Random
      </button>
      <button
        @click="handleDownload"
        class="flex flex-1 items-center justify-center gap-x-2 rounded bg-white py-4 text-xl font-semibold tracking-wide shadow"
      >
        <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 512 512">
          <path
            d="M288 32c0-17.7-14.3-32-32-32s-32 14.3-32 32V274.7l-73.4-73.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3l128 128c12.5 12.5 32.8 12.5 45.3 0l128-128c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L288 274.7V32zM64 352c-35.3 0-64 28.7-64 64v32c0 35.3 28.7 64 64 64H448c35.3 0 64-28.7 64-64V416c0-35.3-28.7-64-64-64H346.5l-45.3 45.3c-25 25-65.5 25-90.5 0L165.5 352H64zm368 56a24 24 0 1 1 0 48 24 24 0 1 1 0-48z"
          />
        </svg>
        Download
      </button>
    </div>
  </div>
</template>
