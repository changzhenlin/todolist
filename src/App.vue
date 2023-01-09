<script setup>
    import {ref,watch} from 'vue'
    let date = localStorage.getItem('tododate')
    let today = new Date().toISOString().substring(0, 10);
    let itemListAll = ref([])
    let allTask = ref([])
    if (!date || date !== today) {
      localStorage.setItem('tododate', today)
    } else {
      if (localStorage.getItem('itemList')) {
        itemListAll.value = JSON.parse(localStorage.getItem('itemList'))
        allTask.value = itemListAll.value
      }
    }
    const newjob = ref('')
    const addJob = () => {
      let obj = {
        name: newjob.value,
        undo: true,
        id: Math.random()
      }
      itemListAll.value.push(obj)
      allTask.value = itemListAll
      localStorage.setItem('itemList', JSON.stringify(itemListAll.value))
      newjob.value = ''
    }
    const handleInput = (e) => {
      newjob.value = e.target.value
    }
    const viewTodo = () => {
      itemListAll.value = allTask.value.filter(item => item.undo === true)
    }
    const viewAll = () => {
      itemListAll.value = allTask.value
    }
    const viewCompleted = () => {
      itemListAll.value = allTask.value.filter(item => item.undo === false)
    }
    // itemList = itemListAll
</script>

<template>
  <header class="bg-gray-600 flex flex-col items-start sm:items-center h-56 p-8 rounded-b-2xl">
    <h1 class="text-2xl text-white">Management <span class="text-blue-400">Task</span></h1>
    <p class="text-white text-md">check your task every day and checked</p>
    <div class="mt-10 overflow-hidden">
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap" @click="viewTodo">Todo</button>
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap" @click="viewCompleted">Completed</button>
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap" @click="viewAll">All task</button>
    </div>
  </header>

  <main class="bg-gray-200">
    <div v-for="item in itemListAll" class="grid m-10 p-4 grid-flow-col text-3xl
    hover:cursor-pointer hover:from-blue-200 hover:to-rose-300 grid-rows-1 grid-cols-2 gap-2 bg-gradient-to-br rounded-2xl from-pink-300 to-rose-300">
      {{ item.name }}
    </div>
    <div class="grid m-10 p-2 grid-flow-row  grid-rows-1 grid-cols-2 gap-1 bg-gradient-to-br rounded-xl from-pink-300 to-rose-300">
      <input type="text" class="p-1" :value="newjob" @input="handleInput" />
      <button class="inline-block w-20 bg-slate-600 h-10 rounded-sm text-white" @click="addJob">添加</button>
    </div>
  </main>
</template>

