<script setup lang="ts">
import { useDark, useToggle } from '@vueuse/core'
import { Sun, Moon } from 'lucide-vue-next'

const isDark = useDark()
const toggleTheme = useToggle(isDark)
</script>

<template>
  <button
    type="button"
    :aria-label="`Toggle theme to ${isDark === true ? 'light' : 'dark'}`"
    class="cursor-pointer"
    @click="() => toggleTheme()"
  >
    <Moon v-if="!isDark" class="min-h-8 min-w-8" />
    <Sun v-else class="min-h-8 min-w-8" />
  </button>
</template>
