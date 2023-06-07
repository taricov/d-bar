<!-- eslint-disable no-console -->
<script setup lang="ts">
import '../styles/main.css'
import { useMagicKeys, whenever } from '@vueuse/core'
import randoms from '~/logic/random-words'
const showBar = ref<boolean>(true)
const isBg = ref<boolean>(false)
const isTransition = ref<boolean>(false)
const spotlight = ref<HTMLInputElement>()
const keys = useMagicKeys()
whenever(keys['ctrl+d'], () => {
  showBar.value = !showBar.value
})

const matches = ref<string[]>([])
const searchList = ref<string[]>(randoms)
const searchValue = ref<string>('')
const onCommand = () => {
  matches.value = []
  console.log(searchValue.value, matches.value)
  matches.value = searchList.value = searchList.value.filter(word => word.toLowerCase().includes(searchValue.value.toLowerCase()))
}
onMounted(() => {
//   onCommand()
  spotlight.value?.focus()
})
</script>

<template>
  <div
    id="dont_change_mystyles"
    class="h-fit flex m-0 space-x-4 items-center justify-center rounded-lg  px-6 py-10 w-6/12 md:w-7/12 mx-auto fixed -top-[1200px] left-1/2 transform -translate-x-1/2 -translate-y-1/2  z-[100] "
    :class="[{ 'top-1/2': showBar }, { ' bg-violet-500 backdrop-blur-[3px] bg-opacity-5 shadow-lg': isBg }, { 'transition-all duration-300': isTransition }]"
  >
    <div class="flex-col overflow-hidden shd grow rounded transition duration-150 min-h-xs max-h-sm bg-gray-600 border-2 border-gray-400">
      <!-- <span class="w-11/12 border-b border-gray-900" /> -->
      <form class="w-full h-full ">
        <input
          ref="spotlight"
          v-model="searchValue"
          type="text"
          placeholder="Command here.."
          class="!font-semibold w-full outline-none m-0 px-3 py-2 h-15 !text-xl block  !text-gray-300  bg-transparent transition duration-150 border-b !border-white !border-opacity-30"
          @input="onCommand"
        >
      </form>
      <!-- <hr class="!border-gray-100 opacity-40  m-auto"> -->
      <div class="scroll-m-0 overflow-y-scroll w-full flex-1 h-[17rem]">
        <ul class="text-gray-200 h-full">
          <li v-for="match in matches" :key="match" class="hover:bg-gray-100 hover:bg-opacity-10 list-none text-left transition duration-200">
            <div
              class="relative px-3 py-3 cursor-pointer after:content-[''] after:hidden after:w-1  after:h-full after:absolute after:top-0
            after:rounded-tr after:rounded-br after:left-0 after:bg-gray-300 hover:after:flex"
            >
              {{ match }}
            </div>
          </li>
        </ul>
      </div>
    </div>
    <!-- <AppDial /> -->
  </div>
</template>
