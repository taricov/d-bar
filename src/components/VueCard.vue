<script setup lang="ts">
import { DeleteNote, UpdateNote } from '~/logic/daftraApi'
defineProps({
  num: Number,
  path: String,
  author: String,
  body: String,
  date: String,
})

let editedNote: any
</script>

<template>
  <v-card
    variant="tonal"
    class="group !bg-slate-900 !text-slate-300 !transition-all duration-300 shadow-lg hover:-translate-y-1 transform !z-10"
  >
    <div class="group-hover:opacity-100 opacity-30 mt-4 transition duration-300">
      Note No. {{ num }}
    </div>
    <v-container class="hover:-translate-x-18 transition duration-300 overflow-hidden trasform absolute !w-fit -right-19 space-y-3 !p-0 bg-slate-50 bg-opacity-5 rounded flex items-center justify-center sapce-x-10 before:content-[''] before:w-2 before:h-8 before:bg-emerald-600">
      <svg class="mx-3 cursor-pointer transition duration-150 hover:fill-emerald-600 fill-sky-400 w-5 p-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" @click="DeleteNote('0')"><path d="M19,4H15.5L14.5,3H9.5L8.5,4H5V6H19M6,19A2,2 0 0,0 8,21H16A2,2 0 0,0 18,19V7H6V19Z" /></svg>
      <svg class="!mt-0 mr-3 cursor-pointer transition duration-150  hover:fill-emerald-600 fill-sky-400 w-4 p-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" @click="UpdateNote('0', editedNote)"><path d="M20.71,7.04C21.1,6.65 21.1,6 20.71,5.63L18.37,3.29C18,2.9 17.35,2.9 16.96,3.29L15.12,5.12L18.87,8.87M3,17.25V21H6.75L17.81,9.93L14.06,6.18L3,17.25Z" /></svg>
    </v-container>

    <v-container class="mt-5">
      <p class="text-lg font-semibold">
        {{ author }}
      </p>
      <p class="italic hover:opacity-100 opacity-50 transition duration-300">
        {{ path }}
      </p>
      <v-chip class="text-md my-2">
        {{ date }}
      </v-chip>
      <p class="text-md px-3 py-2">
        {{ body }}
      </p>
    </v-container>

    <v-card-actions>
      <v-btn :href="path" class="!transition-all !duration-500 !bg-slate-100 !bg-opacity-5 hover:!bg-gradient-to-r hover:!to-emerald-900 hover:!from-sky-700 hover:bg-opacity-50">
        Go to page
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
