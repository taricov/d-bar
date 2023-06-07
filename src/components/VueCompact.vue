<script setup lang="ts">
defineProps({
  path: String,
  author: String,
  date: String,
  body: String,
})
</script>

<template>
  <v-card
    variant="tonal"
    class="!bg-slate-900 !text-slate-300 !transition-all duration-300 shadow-lg hover:-translate-y-1 transform px-1 py-2 text-center"
  >
    <p class="text-md font-semibold">
      {{ author }}
    </p>
    <p class="text-xs italic hover:opacity-100 opacity-50 transition duration-300">
      {{ path }}
    </p>
    <v-chip class="text-xs my-2 ">
      {{ date }}
    </v-chip>
    <p class="text-sm px-3 pb-10 line-clamp-1">
      {{ body }}
    </p>

    <!-- <v-card-actions>
       <v-btn :href="path" class="!transition-all !duration-500 !bg-slate-100 !bg-opacity-5 hover:!bg-gradient-to-r hover:!to-emerald-900 hover:!from-sky-700 hover:bg-opacity-50">
        Go to page
      </v-btn>
    </v-card-actions> -->
  </v-card>

  <!-- <v-card
    class="mx-auto"
    width="400"
    prepend-icon="mdi-home"
  >
    <div>
      {{ date }}
    </div>
    <div>
      {{ author }}
    </div>
    <v-card-text>
      {{ body }}
    </v-card-text>
    <v-button href="path">
      {{ path?.split("/").slice(-1)[0].replace("-", " ") }}
    </v-button>
  </v-card> -->
</template>
