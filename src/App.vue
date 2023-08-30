<script setup lang="ts">
  import {ref} from 'vue'

  const message = ref("Hello world")
</script>

<template>
  <div>
    <h1> {{ message }}</h1>
    <input type="text" v-model="message">
  </div>
</template>

<style scoped>

</style>
