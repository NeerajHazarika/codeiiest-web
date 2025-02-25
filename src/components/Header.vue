<template>
  <Popover open="true" class="relative bg-white dark:bg-dark-900 mb-10 z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6">
      <div class="flex justify-between items-center border-b-2 border-gray-100 dark:border-gray-800 py-6 md:justify-start md:space-x-5">
        <div class="flex justify-start lg:flex-1">
          <a href="https://www.iiests.ac.in/" target="_blank" rel="noreferrer" class="flex-none">
            <img src="/iiest-logo.png" width="80" height="80" />
          </a>
          <router-link to="/">
            <span class="sr-only">CodeIIEST</span>
            <BrandDark v-if="isDark" width="80" height="80" />
            <Brand v-else width="80" height="80" />
          </router-link>
        </div>
        <div class="-mr-2 -my-2 md:hidden">
          <PopoverButton class="bg-white dark:bg-dark-700 rounded-md p-2 inline-flex items-center justify-center text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-red-500  dark:text-gray-300 dark:hover:text-gray-100 dark:hover:bg-dark-800">
            <span class="sr-only">Open menu</span>
            <gridicons-menu class="h-6 w-6" aria-hidden="true" />
          </PopoverButton>
        </div>
        <PopoverGroup as="nav" class="hidden md:flex space-x-5">
          <Popover v-slot="{ open }" class="relative">
            <PopoverButton :class="[open ? 'text-gray-900 dark:text-gray-400' : 'text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100', 'p-1 group bg-white dark:bg-dark-900 rounded-md inline-flex items-center text-base font-medium focus:outline-none focus:ring-2 focus:ring-red-500']">
              <span>Chapters</span>
              <carbon-chevron-down :class="[open ? 'text-gray-600 dark:text-gray-400' : 'text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100', 'ml-2 h-5 w-5 group-hover:text-gray-500 dark:group-hover:text-gray-100']" aria-hidden="true" />
            </PopoverButton>

            <transition
              enter-active-class="transition ease-out duration-200"
              enter-from-class="opacity-0 translate-y-1"
              enter-to-class="opacity-100 translate-y-0"
              leave-active-class="transition ease-in duration-150"
              leave-from-class="opacity-100 translate-y-0"
              leave-to-class="opacity-0 translate-y-1"
            >
              <PopoverPanel class="absolute z-10 -ml-4 mt-3 transform px-2 w-screen max-w-md sm:px-0 lg:ml-0 lg:left-1/2 lg:-translate-x-1/2">
                <div class="rounded-lg shadow-xl shadow-red-700 dark:shadow-red-200 ring-1 ring-black ring-opacity-5 overflow-hidden">
                  <div class="relative grid gap-6 bg-white dark:bg-dark-800 px-5 py-6 sm:gap-8 sm:p-8">
                    <PopoverButton v-for="item in chapters" :key="item.name">
                      <router-link :to="item.route" class="-m-3 p-3 flex items-start rounded-lg hover:bg-gray-100 dark:hover:bg-gray-500">
                        <div class="ml-4">
                          <p class="text-base font-medium text-gray-900 dark:text-gray-200">
                            {{ item.name }}
                          </p>
                        </div>
                      </router-link>
                    </PopoverButton>
                  </div>
                </div>
              </PopoverPanel>
            </transition>
          </Popover>

          <router-link to="/events" class="p-1 text-base font-medium text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100">
            Events
          </router-link>
          <router-link to="/team" class="p-1 text-base font-medium text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100">
            Team
          </router-link>
          <router-link to="/alumni" class="p-1 text-base font-medium text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100">
            Alumni
          </router-link>
        </PopoverGroup>
        <div class="hidden md:flex items-center justify-end md:flex-1 lg:w-0">
          <button class="icon-btn mx-2 flex-none !outline-none" :title="'Toggle Theme'" @click="toggleDark">
            <carbon-moon v-if="isDark" />
            <carbon-sun v-else />
          </button>
        </div>
      </div>
    </div>

    <transition
      enter-active-class="duration-200 ease-out"
      enter-from-class="opacity-0 scale-95"
      enter-to-class="opacity-100 scale-100"
      leave-active-class="duration-100 ease-in"
      leave-from-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-95"
    >
      <PopoverPanel focus class="absolute top-0 inset-x-0 p-2 transition transform origin-top-right md:hidden">
        <div class="rounded-lg shadow-lg shadow-red-700 dark:shadow-red-200 ring-1 ring-black ring-opacity-5 bg-white dark:bg-dark-800 divide-y-2 divide-gray-50 dark:divide-dark-200">
          <div class="pt-5 pb-6 px-5">
            <div class="flex items-center justify-between">
              <div>
                <BrandDark v-if="isDark" width="80" height="80" />
                <Brand v-else width="80" height="80" />
              </div>
              <div class="-mr-2">
                <PopoverButton class="bg-white dark:bg-dark-900 rounded-md p-2 inline-flex items-center justify-center text-gray-400 hover:text-gray-500 hover:bg-gray-100 dark:text-gray-300 dark:hover:text-gray-100 dark:hover:bg-dark-800 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-red-500">
                  <span class="sr-only">Close menu</span>
                  <bi-x class="h-6 w-6" aria-hidden="true" />
                </PopoverButton>
              </div>
            </div>
            <div class="mt-6">
              <nav class="grid gap-y-8">
                <PopoverButton v-for="chapter in chapters" :key="chapter.name">
                  <router-link :to="chapter.route" :aria-label="chapter.name + ' chapter'" class="-m-3 p-3 flex chapters-center rounded-md hover:bg-gray-50 dark:hover:bg-gray-500">
                    <!-- <component :is="chapter.icon" class="flex-shrink-0 h-6 w-6 text-red-600" aria-hidden="true" /> -->
                    <!-- not used right now -->
                    <span class="ml-3 text-base font-medium text-gray-900 dark:text-gray-200">
                      {{ chapter.name }}
                    </span>
                  </router-link>
                </PopoverButton>
              </nav>
            </div>
          </div>
          <div class="py-6 px-5 space-y-6">
            <div class="grid grid-cols-3 gap-y-4 gap-x-8">
              <PopoverButton>
                <router-link to="/events" class="text-base font-medium text-gray-500 dark:text-gray-400 hover:text-gray-800 dark:hover:text-gray-100">
                  Events
                </router-link>
              </PopoverButton>

              <PopoverButton>
                <router-link to="/team" class="text-base font-medium text-gray-500 dark:text-gray-400 hover:text-gray-800 dark:hover:text-gray-100">
                  Team
                </router-link>
              </PopoverButton>

              <PopoverButton>
                <router-link to="/alumni" class="text-base font-medium text-gray-500 dark:text-gray-400 hover:text-gray-800 dark:hover:text-gray-100">
                  Alumni
                </router-link>
              </PopoverButton>
            </div>
            <div>
              <PopoverButton class="icon-btn mx-2 flex-none !outline-none" title="Toggle Theme" aria-label="Dark Theme Switcher" @click="toggleDark">
                <carbon-moon v-if="isDark" />
                <carbon-sun v-else />
              </PopoverButton>
            </div>
          </div>
        </div>
      </PopoverPanel>
    </transition>
  </Popover>
</template>

<script lang="ts">
import { Popover, PopoverButton, PopoverGroup, PopoverPanel } from '@headlessui/vue'
import { isDark, toggleDark, chapters } from '~/logic'

export default {
  components: {
    Popover,
    PopoverButton,
    PopoverGroup,
    PopoverPanel,
  },
  setup() {
    return {
      chapters,
      isDark,
      toggleDark,
    }
  },
}
</script>
