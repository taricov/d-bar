<!-- eslint-disable no-console -->
<script setup lang="ts">
import 'uno.css'
// const showBar
// = ref<boolean>(true)

// const toggleDrawer = (): void => {
// showBar.value = !showBar.value
// noteTextarea.value?.focus()

// console.log('hello', showBar.value)
// }

onMounted(async () => {

})

// const keys = useMagicKeys()
// whenever(keys['ctrl+d'], () => {
//   showBar.value = !showBar.value
// })
// whenever(keys['='], () => {
//   drawer.value = true
//   noteTextarea.value?.focus()
// })
</script>

<template>
  <AppAuto />

  <!-- <div
    class="group fixed flex items-center justify-center right-0 bottom-0 m-5 z-100 font-sans select-none leading-1em w-10 h-10 rounded-full shadow cursor-pointer bg-sky-500 hover:bg-sky-700 transition-all duration-300"
    @click="toggleDrawer"
  >
    <svg class="w-[1.5rem] mt-[3px] ml-[5px] fill-sky-900 group-hover:fill-sky-300" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 118.06 116.67"><defs /><g id="Layer_2" data-name="Layer 2"><g id="Layer_1-2" data-name="Layer 1"><path d="M44.77,90.53H30.4V26.15H44.77Q77,26.15,77,57.68h30.39q0-27-15.2-42.32T50.17,0H0V116.67H50.4V90.3C48.61,90.45,46.75,90.53,44.77,90.53Z" /><path class="cls-1" d="M93,41.63c-1.88,2.18-3.86,4.28-5.61,6.56-1.6,2.08-3,4.33-4.4,6.55-.66,1-1.33,1-2.2.29-1.86-1.46-3.73-2.91-5.65-4.3-1-.71-.92-1.3-.2-2.18,4.07-5,8.24-10,12.11-15.16s7-10.5,10.84-15.52C101.31,13.37,105.19,9.2,109,5a2,2,0,0,1,1.9-.35,32.17,32.17,0,0,1,4.47,3.15c1,.84,1,1.92.24,3.1-1.88,2.93-1.83,3,.88,5.07,1.36,1.06,1.51,1.73.28,3.64-1.81,2.83-3.63,5.68-5.71,8.31A121.24,121.24,0,0,1,94.83,44.44a7.17,7.17,0,0,1-2,.84A20.54,20.54,0,0,1,92.44,43a6.32,6.32,0,0,1,.31-1.52Zm20.09-20.12c-.64-.58-1-.83-1.25-1.14-1.06-1.19-1.8-1-2.65.33a49,49,0,0,1-3.41,4.35c-3.72,4.44-7.46,8.85-11.19,13.28a14.06,14.06,0,0,0-.85,1.3,7,7,0,0,0,6-2.63c2-2.32,4.31-4.32,6.3-6.62C108.44,27.52,110.7,24.5,113.08,21.51Z" /><path class="cls-1" d="M74.13,50.72c2.37,1.8,4.73,3.54,7,5.38.23.19.19,1.09-.05,1.46A122.67,122.67,0,0,1,66.42,76.48a26.17,26.17,0,0,1-2.77,2.8,2.64,2.64,0,0,1-2.18.49,17.27,17.27,0,0,1-3.75-2.5c-1.28-1.09-1.27-2.31-.37-3.85A122.89,122.89,0,0,1,74.13,50.72Z" /><path class="cls-1" d="M55.41,77.4l5.73,4.3c-2.34,3.19-6.29,4.68-10,7.13C52.62,84.7,52.85,80.48,55.41,77.4Z" /></g></g></svg>
  </div> -->
  <!-- <v-layout>
    <v-container class="w-full"> -->
  <!-- <AppAutocomplete :show-bar="showBar" /> -->
  <!-- </v-container>
  </v-layout> -->

  <!-- <v-layout>
    <v-navigation-drawer
      v-model="drawer"
      width="600"
      elevation="9"
      location="right"
      temporary
      class="!bg-gray-900 py-3 px-1"
    >
      <v-container>
        <h3 class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400 text-xl font-extrabold md:text-xl lg:text-3xl dark:text-white">
          Recent Notes
        </h3>
        <v-chip variant="tonal" class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400 px-0 mb-4 text-xl font-extrabold  dark:text-white">
          Free and Open Source Tool
        </v-chip>
        <v-tabs
          v-model="tabs"
          fixed-tabs
        >
          <v-tab
            v-ripple="false"
            class="bg-sky-500 hover:!bg-sky-600 active:!bg-transparent transition duration-300" value="recently-added"
            variant="outlined"
          >
            Recently Added
          </v-tab>
          <v-tab
            v-ripple="false"
            class="bg-sky-500 hover:!bg-sky-600 transition duration-300" value="page-notes"
            variant="outlined"
          >
            Page Notes
          </v-tab>
        </v-tabs>
        <v-window v-model="tabs">
          <v-window-item
            value="page-notes"
          >
            <v-container class="!bg-slate-100 !bg-opacity-2">
              <v-row no-gutters>
                <v-col
                  v-for="note in filtered.slice(0, 2)"
                  :key="note.id"
                  cols="6"
                  sm="4"
                >
                  <VueCompact class="m-2" :body="note.body" :author="note.author" :date="note.date" :path="note.path" />
                </v-col>
              </v-row>
            </v-container>
          </v-window-item>
          <v-window-item
            value="recently-added"
          >
            <v-container class="!bg-slate-100 !bg-opacity-2">
              <v-row no-gutters>
                <v-col
                  v-for="note in notes.slice(0, 6)"
                  :key="note.id"
                  cols="6"
                  sm="4"
                >
                  <VueCompact class="m-2" :body="note.body" :author="note.author" :date="note.date" :path="note.path" />
                </v-col>
              </v-row>
            </v-container>
          </v-window-item>
        </v-window>
        <v-container class="!bg-slate-100 !bg-opacity-2"> -->
  <!-- <v-text size="x-small" class="text-xs hover:opacity-50 text-sky-100 bg-opacity-1 mx-3 cursor-pointer transition duration-300 font-normal" @click="openOptionsPage">
            Go to all notes..
          </v-text>
          <button class="btn mt-2" @click="openOptionsPage">
            Options
          </button>
  </v-container>
  <v-container fluid>
    <form ref="form" @submit.prevent="addNote">
      <v-textarea
        ref="noteTextarea"
        v-model="newNote"
        required
        no-resize
        label="Press Shift + Enter to add notes"
        variant="outlined"
        class="text-gray-200"
        :loading="isLoading"
        @keyup.enter="addNote"
      />
    </form>
  </v-container>
  </v-navigation-drawer>
  </v-layout> -->
  <!-- </v-layout> -->
</template>
