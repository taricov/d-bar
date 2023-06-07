<!-- eslint-disable unused-imports/no-unused-vars -->
<script setup lang="ts">
// import type { SecretsType } from '../logic/types'
// import { CreateUser } from '../logic/dbSDK'
/* eslint no-console: */
// const panel = ref<number[]>([1, 0])
const isDisabled = ref<boolean>(false)
const isConnected = ref<boolean>(false)
const snackbar = ref<boolean>(false)
const connectPanel = ref<Array<String>>([])
const freshInstall = ref<boolean>(true)
const loading = ref<boolean>(false)
const accountKeys = ref<any>({
  sub_domain: '',
  apiKey: '',
  noteModuleKey: '',
  businessName: '',
  theme: 'dark',
  lang: 'en',
  connectionStatus: true,
  notesCount: 0,
})

// onMounted(async () => {
//   try {
//     isConnected.value = true
//     const { sub_domain, noteModuleKey, apiKey } = getSecrets()
//     if (!sub_domain)
//       isConnected.value = false
//     accountKeys.value.noteModuleKey = noteModuleKey
//     accountKeys.value.sub_domain = sub_domain
//     accountKeys.value.apiKey = apiKey
//     const testConn = await GetNotes()
//     loading.value = true
//     if (!testConn.ok)
//       isConnected.value = false
//     console.log('we r live!')
//   }
//   catch (err) {
//     console.error(err)
//   }
//   finally {
//     if (!getSecrets())
//       isConnected.value = false
//   }
// })
// async function submit() {
//   // loading...
//   loading.value = true
//   const { sub_domain, apiKey } = accountKeys.value
//   // Site info based on user inputs

//   // const siteData = await GetSiteInfo({ sub_domain, apiKey })
//   // const { id, business_name, first_name, last_name, subdomain, address1, address2, city, state, phone1, phone2, country_code, currency_code, email, bn1 } = await siteData.data.Site

//   try {
//     const noteModule = await CreateNoteModule({ sub_domain, apiKey })
//     console.log(noteModule)
//   }
//   catch (err) {
//     console.log(err, 'Something went wrong! Please try again')
//   }
//   // Fetching module entity_key
//   const noteModuleKey = await GetAllWorkflows({ sub_domain, apiKey })
//   accountKeys.value.noteModuleKey = noteModuleKey.data[0].entity_key

//   // const userCreated = await CreateUser({ daftra_site_id: `${id}`, business_name, first_name, last_name, subdomain: subdomain.split('.')[0], address1, address2, city, state, phone1, phone2, lang: 'en', country_code, currency_code, email, bn1, api_key: accountKeys.value.apiKey, note_module_key: accountKeys.value.noteModuleKey, prefer_dark: true })

//   // if (userCreated.ok) {
//   //   isConnected.value = true
//   //   loading.value = false
//   //   connectPanel.value = []
//   //   console.log('all set!')
//   // }
// }
</script>

<template>
  <v-snackbar
    v-model="snackbar"
    multi-line
    class="z-[1000000]"
    timeout="5000"
    color="light-blue-darken-4"
  >
    <div class="font-bold">
      You are connected!
    </div>
    <div class="">
      This button is disabled for security reasons and will not be re-activated unless you reset the connection from the lock 🔐 button.
    </div>

    <template #actions>
      <v-btn
        class="!bg-sky-300 !bg-opacity-50 !text-emerald-900"
        variant="text"
        @click="snackbar = false"
      >
        Close
      </v-btn>
    </template>
  </v-snackbar>
  <v-expansion-panels
    v-model="connectPanel"
    :disabled="isDisabled"
    :readonly="isConnected"
    class="!w-9/12 m-auto !bg-opacity-5 mb-5"
  >
    <v-expansion-panel value="connect" class="!bg-opacity-5 !bg-sky-100 !text-sky-200">
      <v-expansion-panel-title expand-icon="false" collapse-icon="false" class="bg-opacity-20 !text-center" @click="isConnected ? snackbar = true : snackbar = false">
        <div v-if="isConnected" class="w-full text-center flex items-center justify-center space-x-2 ml-5">
          <b>Connected
          </b>
          <span class="m-0">
            <svg class="w-6 fill-emerald-600 rounded-full bg-emerald-600 bg-opacity-5 p-1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><title>Connected</title><path d="M21,7L9,19L3.5,13.5L4.91,12.09L9,16.17L19.59,5.59L21,7Z" /></svg>
          </span>
        </div>
        <div v-if="!isConnected" class="w-full text-center">
          Connect
        </div>
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <v-sheet max-width="1000" class="mx-auto bg-transparent ">
          <v-form validate-on="submit lazy" @submit.prevent="">
            <v-text-field
              v-model="accountKeys.sub_domain"
              label="Daftra Subdomain"
              variant="underlined"
            />
            <v-text-field
              v-model="accountKeys.apiKey"
              label="Api Key"
              variant="underlined"
            />

            <v-switch v-model="freshInstall">
              <template #label>
                First time to use?&nbsp;<span>{{ freshInstall ? "Yes" : "No" }}</span>
                <!-- <v-progress-circular
                  :indeterminate="!freshInstall"
                  size="24"
                  class="ms-2"
                /> -->
              </template>
            </v-switch>

            <v-text-field
              v-if="!freshInstall"
              v-model="accountKeys.noteModuleKey"
              label="Module Key"
              variant="underlined"
            />

            <v-btn
              :loading="loading"
              type="submit"
              variant="text"
              block
              class="mt-2"
              text="Submit"
            />
          </v-form>
        </v-sheet>
      </v-expansion-panel-text>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<style scoped>
/* .v-expansion-panel-title__overlay{
    @apply !text-center
} */
</style>
