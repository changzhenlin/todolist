<script setup>
import {ref} from 'vue'
    const newjob = ref('')
    const itemList = ref([])
    const addJob = () => {
      itemList.value.push({
        name: newjob.value,
        undo: true,
        id: Math.random()
      })
      newjob.value = ''
    }
    const handleInput = (e) => {
      newjob.value = e.target.value
    }
</script>

<template>
  <header class="bg-gray-600 flex flex-col items-start sm:items-center h-56 p-8 rounded-b-2xl">
    <h1 class="text-2xl text-white">Management <span class="text-blue-400">Task</span></h1>
    <p class="text-white text-md">check your task every day and checked</p>
    <div class="mt-10 overflow-hidden">
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap">Todo</button>
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap">Completed</button>
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap">All task</button>
    </div>
  </header>

  <main class="bg-gray-200">
    <div class="grid m-10 p-2 grid-flow-col grid-rows-2 grid-cols-3 gap-4 bg-gradient-to-br rounded-2xl from-pink-300 to-rose-300">
      <input type="text" :value="newjob" @input="handleInput" />
      <button @click="addJob">添加</button>
    </div>
    <div v-for="item in itemList" class="grid m-10 p-2 grid-flow-col grid-rows-2 grid-cols-3 gap-4 bg-gradient-to-br rounded-2xl from-pink-300 to-rose-300">
      {{ item.name }}
    </div>
  </main>
</template>

