<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import ColorModeButton from './components/ColorModeButton.vue'
import { Menu, ArrowRight, ArrowDownCircle } from 'lucide-vue-next'
import IconFav from './components/icons/IconFav.vue'

const navigationLinks = [
  { label: 'home' },
  { label: 'projects' },
  { label: 'experience' },
  { label: 'about' },
  { label: 'contact' }
]

const scrollToSection = (label: string) => {
  globalThis.document.getElementById(label)?.scrollIntoView({ behavior: 'smooth' })
  window.history.pushState(null, '', `#${label}`)
}

const showMobileNavigation = ref(false)

const lgMediaQuery = globalThis.matchMedia?.('(min-width: 1024px)')

const handleMediaChange = (e: MediaQueryListEvent) => {
  showMobileNavigation.value = e.matches
}

onMounted(() => {
  if (lgMediaQuery?.matches) {
    showMobileNavigation.value = true
  }
  lgMediaQuery?.addEventListener('change', handleMediaChange)
})

onUnmounted(() => {
  lgMediaQuery?.removeEventListener('change', handleMediaChange)
})

const year = new Date().getFullYear()
</script>

<template>
  <header class="z-50 flex min-h-12 items-start justify-center sm:mx-4 lg:min-h-24">
    <nav
      class="border-white-soft dark:border-black-soft flex max-w-6xl min-w-full items-center justify-between gap-2 rounded-b-xl border bg-white px-2 py-2 sm:px-4 dark:bg-black"
    >
      <div class="flex gap-4">
        <a
          href="/"
          class="flex items-center gap-2 font-serif text-2xl text-amber-500 uppercase text-shadow-xs"
          ><IconFav class="size-8 min-h-8 min-w-8" />Example</a
        >
        <div
          class="bottom-0 left-0 z-50 flex p-2 transition-transform duration-500 ease-in-out not-lg:fixed not-lg:right-0 not-lg:flex-col not-lg:border-t not-lg:bg-white lg:gap-6 dark:not-lg:bg-black"
          :class="showMobileNavigation ? 'not-lg:translate-y-0' : 'not-lg:translate-y-full'"
        >
          <a
            v-for="link in navigationLinks"
            :key="link.label"
            href="#"
            @click.prevent="(scrollToSection(link.label), (showMobileNavigation = false))"
            class="border-amber-500 leading-none capitalize not-lg:border-b not-lg:py-4 lg:border-l lg:px-2"
            >{{ link.label }}</a
          >
        </div>
      </div>

      <div>
        <ColorModeButton />

        <button
          @click="showMobileNavigation = !showMobileNavigation"
          class="lg:hidden"
          aria-label="Open navigation drawer"
        >
          <Menu class="min-h-8 min-w-8" />
        </button>
      </div>
    </nav>
  </header>

  <main class="">
    <section id="home" class="bg-[url(/background.webp)] bg-cover bg-center">
      <div
        class="flex w-full flex-col justify-center gap-6 bg-white/80 py-4 backdrop-blur-xs sm:px-4 dark:bg-black/80"
      >
        <div class="flex justify-center">
          <div
            class="flex w-full items-center gap-4 not-lg:flex-col lg:max-w-[80%] lg:justify-between lg:px-2"
          >
            <img
              class="aspect-video size-full max-w-126 rounded-lg object-cover shadow"
              src="/profile.webp"
              alt="Profile"
            />
            <div class="flex gap-2 lg:flex-col">
              <a
                href="/#contact"
                class="rounded-sm bg-amber-500 p-2 font-mono leading-none font-medium lg:p-4 lg:text-xl"
              >
                Get in touch <ArrowRight class="invert" />
              </a>
              <a
                href="/#projects"
                class="rounded-sm border-2 p-2 font-mono leading-none font-medium text-amber-500 backdrop-blur-xs lg:p-4 lg:text-xl"
              >
                See live demo <ArrowRight />
              </a>
            </div>
          </div>
        </div>

        <div class="flex justify-center">
          <div class="w-full space-y-4 px-2 sm:space-y-8 lg:max-w-[80%]">
            <p
              class="size-fit rounded-full bg-white/50 p-2 text-xl leading-none font-medium text-balance text-amber-500 uppercase shadow backdrop-blur-xs text-shadow-xs not-sm:text-center lg:text-2xl dark:bg-black/50"
            >
              Make your first impression work for you
            </p>

            <div class="flex flex-col">
              <h1 class="font-serif text-4xl text-balance not-sm:text-center lg:text-6xl">
                Personal <i>Portfolio</i> Website
              </h1>
              <div class="flex gap-2 not-lg:flex-col">
                <span
                  class="shrink-0 text-sm leading-none text-balance text-amber-700 not-sm:text-center"
                  >A clean starting point for your online presence
                </span>
                <div aria-hidden="true" class="w-full self-center border-b border-amber-700" />
              </div>
            </div>

            <p class="text-prett text-base leading-relaxed not-sm:text-center lg:text-lg">
              Sample portfolio website for a freelancer or professional, showcasing skills, selected
              work, and a simple contact section with a focus on clarity and usability.
            </p>
          </div>
        </div>
      </div>
    </section>

    <a
      href="/projects"
      @click.prevent="scrollToSection('projects')"
      class="animate-ease-in my-2 flex animate-bounce items-center justify-center gap-2 text-sm select-none"
    >
      Scroll down <ArrowDownCircle class="size-4" />
    </a>

    <section class="min-h-80"></section>
  </main>

  <footer class="min-h-16 min-w-full">
    <small class="text-sm">&copy; {{ year }} Example Portfolio Website</small>
  </footer>
</template>

<style scoped></style>
