<!-- eslint-disable no-console -->
<script setup lang="ts">
import '../styles/main.css'
import { useMagicKeys, whenever } from '@vueuse/core'
import randoms from '~/logic/random-words'
const showBar = ref<boolean>(false)
const isBg = ref<boolean>(true)
const loading = ref<boolean>(false)
const autoComplete = ref()
const isTransition = ref<boolean>(true)
const spotlight = ref<HTMLInputElement>()
const queryLabel = ref<String | null>(null)
// const queryKeys = ref<any>({
//   goto: '/',
//   new: '+',
//   help: '?',
// })
const keys = useMagicKeys()
whenever(keys['ctrl+/'], () => {
  showBar.value = !showBar.value
})

const matches = ref<{ [key: string]: string }>({})
const searchList = ref<any>(randoms)
const searchValue = ref<string>('')
const onSelect = () => {
  // console.log(searchValue.value, matches.value)
}
const onSubmit = () => {
  // console.log(searchValue.value, matches.value)
}

// const getKeyByValue = (object: { [x: string]: any }, value: string | null) => Object.keys(object).find(key => object[key] === value)

// function getKeyByValue(object: { [x: string]: any; hasOwnProperty: (arg0: string) => any }, value: any) {
//   for (const prop in object) {
//     // eslint-disable-next-line no-prototype-builtins
//     if (object.hasOwnProperty(prop)) {
//       if (object[prop] === value)
//         return prop
//     }
//   }
// }
const addLabel = () => {
  const q = searchValue.value
  if (q.length === 1 && q[0] === '/')
    return 'go to'
}
const onQuery = () => {
  const l = searchList.value
  const label = addLabel()
  matches.value = {}
  loading.value = true
  setTimeout(() => loading.value = false, 1000)
  if (label?.length) {
    // searchValue.value = searchValue.value.length > 1 ? searchValue.value.slice(1) : searchValue.value
    console.log(searchValue.value)
    if (label === 'go to') {
      queryLabel.value = label

      matches.value = searchValue.value.length === 1
        ? l.routes
        : l.filter((word: string) => {
          console.log(searchValue.value.slice(1))
          return word.toLowerCase().includes(searchValue.value.slice(1).toLowerCase())
        })
    }
  }
  if (!searchValue.value.length) {
    queryLabel.value = null
    matches.value = {}
  }

  // ).map(route => route.split('_').join(' '))
  //   .filter((word) => {
  //   console.log(word.toLowerCase(), q.toLowerCase())
  //   return word.toLowerCase().includes(q.toLowerCase())
  // }
}

onMounted(() => {
  autoComplete.value = 'fefefe'
  //   onCommand()
  spotlight.value?.focus()
})
</script>

<template>
  <div
    id="dont_change_mystyles"
    class="h-fit flex m-0 space-x-4 items-center justify-center rounded-lg px-6 py-10 w-6/12 md:w-7/12 mx-auto fixed -top-[1200px] left-1/2 transform -translate-x-1/2 -translate-y-1/2 z-[100]"
    :class="[
      { 'top-1/2': showBar },
      { 'transition-all duration-300': isTransition },
    ]"
  >
    <div
      :class="{ ' bg-violet-500 backdrop-blur-[3px] bg-opacity-5 shadow-lg fixed w-screen h-screen': isBg }" @click="showBar = false"
    />
    <div
      class="z-1 flex-col overflow-hidden shd grow rounded transition duration-150 max-h-sm bg-gray-600 border-2 border-gray-400"
    >
      <!-- <span class="w-11/12 border-b border-gray-900" /> -->
      <form class="relative flex w-full h-full" @submit.prevent="onSubmit">
        <div v-if="loading" class="loader" />
        <div v-if="queryLabel" class="w-20 special-label-container bg-sky-600 px-3 flex justify-center items-center">
          <div class="special-label">
            {{ queryLabel }}
          </div>
        </div>
        <div class="w-full flex">
          <input
            ref="spotlight"
            v-model="searchValue"
            type="text"
            placeholder="Command here.."
            class="relative !font-semibold grow outline-none m-0 px-3 py-2 h-11 !text-xl block !text-gray-300 bg-transparent transition duration-150 !border-none"
            @input="onQuery"
          >
        </div>
        <span
          ref="autoComplete"
          class="absolute flex items-center justify-start top-1/2 px-3 !left-0 transform -translate-y-1/2 font-semibold outline-none h-15 text-xl text-gray-300/30 bg-transparent transition duration-150"
        >{{ "" }}</span>
      </form>
      <hr class="border-t-light-50/20 border-b-none m-0">
      <!-- <hr class="!border-gray-100 opacity-40  m-auto"> -->
      <div
        :class="{ hidden: !Object.keys(matches).length }"
        class="scroll-m-0 overflow-y-scroll w-full flex-1 h-[17rem]"
      >
        <ul class="text-gray-200 h-full my-0 p-0">
          <li
            v-for="(v, k) in matches"
            :key="k"
            :data-val="v"
            tabindex="0"
            class="hover:bg-gray-100 hover:bg-opacity-10 list-none text-left transition duration-200"
          >
            <div
              :data-val="v"
              class="relative px-3 py-3 cursor-pointer after:content-[''] after:hidden after:w-1 after:h-full after:absolute after:top-0 after:rounded-tr after:rounded-br after:left-0 after:bg-gray-300 hover:after:flex"
              @click="onSelect"
            >
              {{ (`${k}`)
                .split("_")
                .join(" ")
                .toLowerCase()
                .split(" ")
                .map((word) => word.charAt(0).toUpperCase() + word.substring(1))
                .join(" ") }}
            </div>
          </li>
        </ul>
      </div>
    </div>
    <!-- <AppDial /> -->
  </div>
</template>

<style>
.special-label-container {
  /* position: fixed;
    top: 65px;
    left: 45px;
    padding: 3px; */
    width: 20%;

  }
  .special-label {
    /* border-radius: 4px;
    padding: 3px;*/
    text-transform: uppercase;
    color: #ddd;
    font-size: 15px;
    font-weight: 600;
    /* background: #c1ccca45; */
}
.loader {
  position: fixed;
    top: 60px;
    right: 45px;
    width: 25px;
    padding: 5px;
    aspect-ratio: 1;
    border-radius: 50%;
    background: #c1ccca;
    --_m: conic-gradient(#0000 10%,#000), linear-gradient(#000 0 0) content-box;
    -webkit-mask: var(--_m);
    mask: var(--_m);
    -webkit-mask-composite: source-out;
    mask-composite: subtract;
    animation: l3 1s infinite linear;
}
@keyframes l3 {to{transform: rotate(1turn)}}
</style>
