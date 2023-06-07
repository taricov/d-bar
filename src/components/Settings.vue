<!-- eslint-disable no-console -->
<script setup lang="ts">
import { getSecrets } from '~/logic/utils'

defineProps({ openSettings: Boolean })
const connected = ref<boolean>(false)

const businessNameKnown = ref<string | null>(null)
const currtheme = ref<string | null>(null)
const currLang = ref<string>('en')

onMounted(() => {
  try {
    const { subdomain, businessName, apiKey, noteModuleKey, theme } = getSecrets() || null
    console.log(businessName)

    businessNameKnown.value = businessName || 'Notes'
    currtheme.value = theme || 'dark'
    connected.value = !!noteModuleKey
  }
  catch (err) {
    console.error(err)
  }
})

const toggleTheme = () => {
  currtheme.value === 'dark' ? currtheme.value = 'light' : currtheme.value = 'dark'
  // eslint-disable-next-line no-console
  console.log(currtheme.value)
}
const toggleLang = () => {
  currLang.value === 'en' ? currLang.value = 'ar' : currLang.value = 'en'
  // eslint-disable-next-line no-console
  console.log(currLang.value)
}
const resetWarning = ref<Boolean>(false)
const resetSecrets = () => {
  resetWarning.value = false
  localStorage.removeItem('connector-data')
}
</script>

<template>
  <v-dialog
    transition="dialog-top-transition"
    width="50%"
    :is-active="openSettings"
    class=""
  >
    <v-snackbar
      v-model="resetWarning"
      multi-line
      class="z-[1000000]"
      timeout="5000"
      color="red-darken-3"
    >
      <div class="font-bold text-yellow-400">
        Warning!
      </div>
      <div class="">
        This button will reset the connection and remove your securely saved credentials. If you still want to revok the connection, Double click the lock button.
      </div>
    </v-snackbar>
    <v-card class="!bg-gray-900 shadow-lg">
      <v-container class="flex justify-between">
        <div>
          <h3 class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400 text-xl font-extrabold md:text-xl lg:text-3xl dark:text-white">
            Settings
          </h3>
          <p variant="tonal" class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400 px-0 mb-4 text-xl font-extrabold  dark:text-white">
            Connet your Daftra
          <!-- and cusomize the look to your likings -->
          </p>
        </div>
        <v-btn class="group !opacity-40 w-fit !bg-opacity-5 !shadow-none hover:shadow-lg transition duration-300 !bg-sky-200 overflow-hidden" @click="resetWarning = true" @dblclick="resetSecrets">
          <svg class="group-hover:fill-red-400 fill-sky-400 transition duration-300 w-7 mt-[.1rem]" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><title>Reset Connection</title><path d="M12.63,2C18.16,2 22.64,6.5 22.64,12C22.64,17.5 18.16,22 12.63,22C9.12,22 6.05,20.18 4.26,17.43L5.84,16.18C7.25,18.47 9.76,20 12.64,20A8,8 0 0,0 20.64,12A8,8 0 0,0 12.64,4C8.56,4 5.2,7.06 4.71,11H7.47L3.73,14.73L0,11H2.69C3.19,5.95 7.45,2 12.63,2M15.59,10.24C16.09,10.25 16.5,10.65 16.5,11.16V15.77C16.5,16.27 16.09,16.69 15.58,16.69H10.05C9.54,16.69 9.13,16.27 9.13,15.77V11.16C9.13,10.65 9.54,10.25 10.04,10.24V9.23C10.04,7.7 11.29,6.46 12.81,6.46C14.34,6.46 15.59,7.7 15.59,9.23V10.24M12.81,7.86C12.06,7.86 11.44,8.47 11.44,9.23V10.24H14.19V9.23C14.19,8.47 13.57,7.86 12.81,7.86Z" /></svg>
        </v-btn>
      </v-container>
      <v-container class="!relative flex space-x-5 items-center justify-center bg-sky-100 bg-opacity-5 rounded my-3 !w-8/12">
        <v-btn disabled class="!opacity-40 w-fit !bg-opacity-5 !shadow-none hover:shadow-lg transition duration-300 !bg-sky-200 overflow-hidden" @click="toggleTheme">
          <span>
            <!-- <transition> -->
            <svg v-if="currtheme === 'dark'" class="fill-sky-400 transition duration-300 w-7 mt-[.1rem]" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><title>Dark Mode</title><path d="M3.55 19.09L4.96 20.5L6.76 18.71L5.34 17.29M12 6C8.69 6 6 8.69 6 12S8.69 18 12 18 18 15.31 18 12C18 8.68 15.31 6 12 6M20 13H23V11H20M17.24 18.71L19.04 20.5L20.45 19.09L18.66 17.29M20.45 5L19.04 3.6L17.24 5.39L18.66 6.81M13 1H11V4H13M6.76 5.39L4.96 3.6L3.55 5L5.34 6.81L6.76 5.39M1 13H4V11H1M13 20H11V23H13" /></svg>
            <svg v-if="currtheme !== 'dark'" class="fill-sky-400 w-7" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><title>Light Mode</title><path d="M2 12A10 10 0 0 0 15 21.54A10 10 0 0 1 15 2.46A10 10 0 0 0 2 12Z" /></svg>
            <!-- </transition> -->
          </span>
          <v-tooltip
            activator="parent"
            location="top"
            transition="false"
          >
            {{ `Theme: ${currtheme}` }}
          </v-tooltip>
        </v-btn>
        <v-btn disabled class="!opacity-40 w-fit !bg-opacity-5 !shadow-none hover:shadow-lg transition duration-300 !bg-sky-200 overflow-hidden" @click="toggleLang">
          <span class="text-sky-500 text-md font-bold">
            {{ currLang === 'en' ? 'En' : 'عربي' }}
          </span>
          <v-tooltip
            activator="parent"
            location="top"
            transition="false"
          >
            {{ `Language: ${currLang}` }}
          </v-tooltip>
        </v-btn>
        <v-btn disabled class="!opacity-40 w-fit !bg-opacity-5 !shadow-none hover:shadow-lg transition duration-300 !bg-sky-200 overflow-hidden" href="/">
          <span class="text-sky-500 font-bold">
            How to use
          </span>
          <v-tooltip
            activator="parent"
            location="top"
            transition="false"
          >
            {{ `Language: ${currLang}` }}
          </v-tooltip>
        </v-btn>
        <div variant="plain" class="rounded-full bg-gradient-to-r from-emerald-400 to-sky-600 text-slate-800 px-3 py-1 transform -translate-x-1/2 -translate-y-1/2 !absolute !left-1/2 !top-1/12 text-xs font-bold mx-0">
          Coming Soon
        </div>
      </v-container>
      <v-card-text>
        <Connector />
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<style scoped>
.v-dialog.v-overlay{
  @apply !bg-gray-100 !bg-opacity-10
}
</style>
