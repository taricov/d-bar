<!-- eslint-disable no-console -->
<script setup lang="ts">
import AutoComplete from 'primevue/autocomplete'
import { ref } from 'vue'
import { useToast } from 'primevue/usetoast'
import SpeedDial from 'primevue/speeddial'
import { useRouter } from 'vue-router'

defineProps({
  showBar: Boolean,
})
const toast = useToast()
const router = useRouter()

const itemsDial = ref([
  {
    label: 'Add',
    icon: 'pi pi-pencil',
    command: () => {
      toast.add({ severity: 'info', summary: 'Add', detail: 'Data Added' })
    },
  },
  {
    label: 'Update',
    icon: 'pi pi-refresh',
    command: () => {
      toast.add({ severity: 'success', summary: 'Update', detail: 'Data Updated' })
    },
  },
  {
    label: 'Delete',
    icon: 'pi pi-trash',
    command: () => {
      toast.add({ severity: 'error', summary: 'Delete', detail: 'Data Deleted' })
    },
  },
  {
    label: 'Upload',
    icon: 'pi pi-upload',
    command: () => {
      router.push('/fileupload')
    },
  },
  {
    label: 'Vue Website',
    icon: 'pi pi-external-link',
    command: () => {
      window.location.href = 'https://vuejs.org/'
    },
  },
])

const value = ref<string>('')
const items = ref<Array<string>>([])

const search = (event: any) => {
  items.value = [...Array(10).keys()].map(item => `${event.query}-${item}`)
}
</script>

<template>
  <div
    class="h-fit flex items-center justify-center rounded-lg shadow-lg px-6 py-10 bg-violet-500 backdrop-blur-[3px] bg-opacity-5 w-10/12 mx-auto fixed -top-[1200px] left-1/2 transform -translate-x-1/2 -translate-y-1/2  z-[100] transition-top duration-300"
    :class="{ 'top-1/2': showBar }"
  >
    <AutoComplete
      v-model="value"
      :suggestions="items"
      @complete="search"
    />
    <div class="card" :style="{ position: 'relative', height: '500px' }">
      <SpeedDial :model="itemsDial" :radius="80" type="semi-circle" direction="right" :style="{ top: 'calc(50% - 2rem)', right: 0 }" />
    </div>
  </div>
</template>

<style scoped>
.p-inputtext {
    @apply  !w-10/12
}
</style>
