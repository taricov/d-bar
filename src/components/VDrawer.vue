<script lang="ts" setup>
const props = defineProps({ drawer: Boolean })
/* eslint no-console: */
console.log('from props: ', props.drawer)
</script>

<template>
  <!-- <el-drawer :drawer="drawer" title="I am the title" :with-header="false">
    <span>Hi there!</span>
  </el-drawer> -->
  <v-app>
    <v-navigation-drawer
      :tog="props.drawer"
      location="right"
      temporary
    >
      <p>hello</p>
    </v-navigation-drawer>
  </v-app>
</template>
