<script setup lang="ts">
  import { ref, computed } from 'vue'

  const message = ref("Welcome to this tutorial with Elvin Code");
  const showFormular = ref(false);
  const tasks = ref([
    { id: 1, label: "Bonjour", purchased: false, level: 0 },
    { id: 2, label: "Elvin", purchased: true, level: 2 },
  ]);
  const sortedTasks = computed(() => {
    return tasks.value.sort((a, b) => b.level - a.level);
  });
  const newTaskValue = ref("");
  const newTaskPriority = ref(false);
  const editingIndex = ref(-1);

  const addingTask = () => {
    tasks.value.push({
      id: tasks.value.length + 1,
      label: newTaskValue.value,
      purchased: false,
      level: newTaskPriority.value ? 2 : 0
    });
    sortedTasks.value;
    newTaskValue.value = "";
    newTaskPriority.value = false;
  };

  const editingTask = (index) => {
    showFormular.value = true;
    newTaskValue.value = tasks.value[index].label;
    editingIndex.value = index;
  };

  const deleteTasks = (index)=>{
    tasks.value.splice(index, 1);
  }
  const saveTask = () => {
    tasks.value[editingIndex.value].label = newTaskValue.value;
    showFormular.value = false;
    newTaskValue.value = "";
    editingIndex.value = -1;
  };

  const togglePurchased = (item) => {
    item.purchased = !item.purchased;
  };
</script>

<template>
  <div class="flex justify-center flex-col min-h-screen items-center">
    <h1 class="text-xl">{{ message }}</h1>
    <form 
      @submit.prevent="editingIndex !== -1 ? saveTask() : addingTask()" 
      v-if="showFormular" 
      class="w-1/3 min-h-[10rem] bg-slate-300 py-4 px-8 bg mt-3"
    >
      <div>
        <div>
          <div class="mb-6">
            <input 
              v-model="newTaskValue" type="text" 
              class="block w-full p-3 text-gray-900 border 
              border-gray-300 rounded-lg sm:text-md bg-slate-100"
            >
          </div>
        </div>
        <div class="my-4">
          <label for="level">
            High task
            <input type="checkbox" id="level" v-model="newTaskPriority">
          </label>
        </div>
        <div class="flex space-x-4">
          <input type="submit" value="Ajouter" v-if="editingIndex === -1" class="bg-indigo-500 cursor-pointer text-white px-4 py-2 rounded-sm font-semibold">
          <input type="submit" value="Enregistrer" v-else class="bg-indigo-500 cursor-pointer text-white px-4 py-2 rounded-sm font-semibold">
          <button @click="showFormular = false" class="bg-red-500 cursor-pointer text-white px-4 py-2 rounded-sm font-semibold">
            Fermer
          </button>
        </div>
      </div>
    </form>
    <div class="w-1/3 min-h-[10rem] flex flex-col items-center justify-center bg-slate-300 py-4 px-8 bg mt-3">
      <ul class="space-y-4" v-if="tasks.length != 0">
        <li v-for="(item, index) in sortedTasks" :key="item.id" class="p-3 bg-white text-black rounded-md flex justify-between items-center w-96">
          <span class="font-semibold cursor-pointer" :class="{ 'line-through': item.purchased, 'text-red-500': item.level === 2}" @click="togglePurchased(item)">
            {{ index }} {{ item.label }}
          </span>
          <div class="flex gap-2 text-white">
            <button class="bg-red-500 p-2" @click="deleteTasks(index)">Supprimer</button>
            <button class="p-2 bg-indigo-500" @click="editingTask(index)">Editer</button>
          </div>
        </li>
      </ul>
      <div v-else>
        <h1 class="text-center font-extralight text-2xl">
          Il n'y a pas de tâches !
        </h1>
      </div>
      <button @click="showFormular=true" class="bg-indigo-500 mt-3 cursor-pointer text-white px-4 py-2 rounded-sm font-semibold">
        Ajouter une tâche
      </button>
    </div>
  </div>
</template>

<style scoped>
.purchased {
  text-decoration: dashed;
}
</style>
