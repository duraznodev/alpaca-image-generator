<script setup>
defineProps({
  active: Boolean
})
</script>

<template>
  <button
    class="rounded-full border border-blue-500 px-6 py-1.5 text-lg font-semibold capitalize"
    :class="{
      'bg-blue-500 text-white': active,
      'bg-white text-blue-500': !active
    }"
  >
    <slot />
  </button>
</template>
