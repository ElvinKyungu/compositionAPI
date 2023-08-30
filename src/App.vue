<script setup lang="ts">
  import {ref} from 'vue'

  const message = ref("Hello world")
</script>

<template>
  <div>
    <h1 class="text-3xl font-bold underline">
      Hello world!
    </h1>
    <h1> {{ message }}</h1>
    <form>
      <div>
        <div>
          <input type="text">
        </div>
        <div class="">
          <label for="level">
            High task
            <input type="checkbox" id="level" >
          </label>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped>

</style>
