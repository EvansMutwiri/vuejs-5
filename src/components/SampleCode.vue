<template>
<div class="container mx-auto text-center space-y-6 bg-slate-400 p-12 place-items-center">
  <h1 class="font-bold text-xl">My To List</h1>
  <p v-if="toDoList.length > 3" class="bg-red-400 text-yellow-50">Your list is getting long.</p>

  <ul class="bg-slate-100 py-6 w-full">
    <li v-for="(toDo, id) in toDoList" :key="id">{{toDo.id}} - {{ toDo.label }}</li>
  </ul>

  <div class="flex justify-center">
    <form class="px-4" @submit.prevent="addNew">
    <input type="text" class="rounded-md bg-slate-100 p-2 focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500" placeholder="Enter your Task" v-model="newToDo" ref="input">
  </form>

  <button class="bg-sky-400 text-white px-3 rounded-md" @click="addNew"> Add </button>
  </div>
</div>
  
</template>

<script setup>
import { ref } from '@vue/reactivity';
import { onMounted, watch } from '@vue/runtime-core';


    let toDoList = ref([
      {id: 1, label: "Learn Vue"}
    ]);

    let newToDo = ref("");

    const addNew = () => {
      toDoList.value.push({id: toDoList.value.length + 1, label: newToDo.value});
      newToDo.value = null;
    }

    //alert user when they have too many to dos
    watch(toDoList.value, (newValue, oldValue) => {
      if (newValue.length >= 4) {
        alert('Your list is getting long');
      }
    });

    //templete ref
    const input = ref(null)

    onMounted(()=> {
      input.value.focus();
    });

</script>

<style>

</style>