<script setup lang="ts">
  import {ref} from 'vue'

  const message = ref("Hello world");
  const showFormular = ref(false)
  const tasks = ref([
    {id: 1, label: "Bonjoour", level : "high"},
    {id: 1, label: "Bonjoour", level : "high"},
    {id: 1, label: "Bonjoour", level : "high"},
    {id: 1, label: "Bonjoour", level : "high"}
  ])
  const addingTask = ()=>{
    
  }
  
</script>

<template>
  <div class="flex justify-center flex-col h-screen items-center">
    <h1> {{ message }}</h1>
    <form 
      @submit.prevent="addingTask()"
      v-if="showFormular"
      class="w-1/3 min-h-[10rem] bg-slate-300 py-4 px-8 bg mt-3"
    >
      <div>
        <div>
          <input 
            type="text" 
            class="
              w-full bg-slate-100 border 
              border-black rounded-sm py-1 px-4 
            "
          >
        </div>
        <div class="my-4">
          <label for="level">
            High task
            <input type="checkbox" id="level" >
          </label>
        </div>
        <input 
          type="submit" 
          value="Ajouter" 
          class="bg-indigo-500 cursor-pointer text-white px-4 py-2 rounded-sm font-semibold"
        >
      </div>
    </form>
    <div class="w-1/3 min-h-[10rem] flex flex-col items-center justify-center bg-slate-300 py-4 px-8 bg mt-3">
      <ul class="space-y-4" v-if="!tasks.length">
        <li v-for="({id, label}) in tasks" :key="id" class="p-3 bg-white text-black rounded-md flex justify-between items-center">
          <span class="font-semibold">{{ label }}</span>
          <div class="flex gap-2 text-white">
            <button class="bg-red-500 p-2 ">Supprimer</button>
            <button class="p-2 bg-indigo-500">Editer</button>
          </div>
        </li>
      </ul>
      <div>
        <h1 
          class="text-center font-extralight text-2xl"
        >
          Il n'y a pas de tâches !
        </h1>
      </div>
      <button
        @click="showFormular=true"
        class="bg-indigo-500 mt-3 cursor-pointer text-white px-4 py-2 rounded-sm font-semibold"
      >
        Ajouter une tâche
      </button>
    </div>
  </div>
</template>

<style scoped>

</style>
