<script setup>
import AlpacaImage from './components/AlpacaImage.vue'
import Button from './components/Button.vue'
import { variants } from './utils/variants.js'
import { onMounted, ref } from 'vue'

const activePart = ref('hair')

const alpaca = ref({
  hair: 'default',
  ears: 'default',
  eyes: 'default',
  mouth: 'default',
  neck: 'default',
  leg: 'default',
  accesories: null,
  background: 'darkblue70'
})

function randomAlpaca() {
  Object.keys(variants).forEach((part) => {
    alpaca.value[part] = variants[part][Math.floor(Math.random() * variants[part].length)]
  })
}

onMounted(() => {
  randomAlpaca()
})
</script>

<template>
  <div class="flex h-screen items-center justify-center bg-gray-100">
    <div>
      <h1 class="text-5xl font-bold uppercase text-blue-950">Alpaca Generator</h1>
      <div class="mt-6 flex gap-x-12">
        <div>
          <AlpacaImage :alpaca="alpaca" @randomAlpaca="randomAlpaca" />
        </div>
        <div class="max-w-xs">
          <div>
            <span class="text-lg font-bold uppercase text-blue-950">Accessorize the alpaca's</span>
            <div class="mt-2 flex flex-wrap gap-2">
              <Button
                :active="part === activePart"
                @click="activePart = part"
                v-for="part in Object.keys(variants)"
              >
                {{ part }}</Button
              >
            </div>
          </div>
          <div class="mt-6 flex flex-wrap gap-2">
            <span class="text-lg font-bold uppercase text-blue-950">Accessorize the alpaca's</span>
            <div class="mt-2 flex flex-wrap gap-2">
              <Button
                v-if="activePart !== 'background'"
                :active="alpaca[activePart] === part"
                @click="alpaca[activePart] = part"
                v-for="part in variants[activePart]"
                >{{ part }}</Button
              >
              <button class="w-10" v-else v-for="part in variants[activePart]">
                <img
                  @click="alpaca[activePart] = part"
                  :src="`/src/assets/alpaca/backgrounds/${part}.png`"
                  class="relative h-full w-full rounded-md"
                  :class="{
                    '-translate-y-1': alpaca[activePart] === part
                  }"
                />
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
