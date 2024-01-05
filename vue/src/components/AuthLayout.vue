<script setup>
import { ref } from 'vue'


defineProps({
  msg: String,
})

const count = ref(0)
</script>


<template>
  <!--
    This example requires updating your template:

    ```
    <html class="h-full bg-white">
    <body class="h-full">
    ```
  -->
  <div class="flex min-h-full flex-1 flex-col justify-center px-6 py-12 lg:px-8">
   
    <router-view></router-view>
  </div>
</template>


