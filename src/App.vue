<script setup>
    import {ref,watch} from 'vue'
    let date = localStorage.getItem('tododate')
    let today = new Date().toISOString().substring(0, 10);
    let itemListAll = ref([])
    let allTask = ref([])
    let initArrItemList = ref([
      {
        name: '一道力扣',
        undo: true,
        id: Math.random()
      },
      {
        name: '一张ins图',
        undo: true,
        id: Math.random()
      },
      {
        name: '百词斩打卡',
        undo: true,
        id: Math.random()
      },
      {
        name: '一条问答',
        undo: true,
        id: Math.random()
      },
      {
        name: '一个commit',
        undo: true,
        id: Math.random()
      }
    ])
    if (!date || date !== today) {
      localStorage.setItem('tododate', today)
      allTask.value = itemListAll.value = initArrItemList.value
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
      curPage.value = 'todo'
      itemListAll.value = allTask.value.filter(item => item.undo === true)
    }
    const viewAll = () => {
      curPage.value = 'all'
      itemListAll.value = allTask.value
    }
    const viewCompleted = () => {
      curPage.value = 'completed'
      itemListAll.value = allTask.value.filter(item => item.undo === false)
    }
    const taskCheck = (item) => {
      item.undo = !item.undo
      localStorage.setItem("itemList",JSON.stringify(itemListAll.value))
    }
    const taskDelete = (item) => {
      allTask.value = allTask.value.filter(i => i.id !== item.id)
      itemListAll.value = itemListAll.value.filter(i => i.id !== item.id)
      localStorage.setItem("itemList",JSON.stringify(itemListAll.value))
    }
    const curPage = ref('todo')
    const testClass = ref('bg-blue-400')
    const defaultcss = ref('bg-blue-100')
    let todocount = allTask.value.filter(item => item.undo === true).length
    let compledcount = allTask.value.filter(item => item.undo === false).length
    let allcount = allTask.value.length
    watch(curPage, (val) => {
      if (val === 'todo') {
        testClass.value = 'bg-blue-400'
      } else if (val === 'completed') {
        testClass.value = 'bg-pink-400'
      } else if (val === 'all') {
        testClass.value = 'bg-purple-400'
      }
    })
    // itemList = itemListAll
</script>

<template>
  <header class="bg-gray-600 flex flex-col items-start sm:items-center h-56 p-8 rounded-b-2xl">
    <h1 class="text-2xl text-white">Management <span class="text-blue-400">Task</span></h1>
    <p class="text-white text-md">check your task every day and checked</p>
    <div class="mt-10 overflow-hidden">
      <ul class="list-disc">
        <li :class="curPage === 'todo' ? testClass : defaultcss" class="inline text-white rounded-lg px-4 py-2 m-2" @click="viewTodo">Todo{{ todocount }}</li>
        <li :class="curPage === 'completed' ? testClass : defaultcss" class="bg-blue-400 inline text-white rounded-lg px-4 py-2 m-2" @click="viewCompleted">Completed{{ compledcount }}</li> 
        <li :class="curPage === 'all' ? testClass : defaultcss" class="bg-blue-400 inline text-white rounded-lg px-4 py-2 m-2" @click="viewAll">All task{{ allcount }}</li> 
      </ul>
      <!-- <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap" @click="viewTodo">Todo</button>
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap" @click="viewCompleted">Completed</button>
      <button class="bg-blue-400 text-white rounded-lg px-4 py-2 m-2 whitespace-nowrap" @click="viewAll">All task</button> -->
    </div>
  </header>

  <main class="bg-gray-200">
    <div v-for="item in itemListAll" @click="taskCheck(item)" class="m-10 p-4 text-3xl flex justify-between
    hover:cursor-pointer hover:from-blue-200 hover:line-through hover:to-rose-300  gap-2 bg-gradient-to-br rounded-2xl from-pink-300 to-rose-300">
      <span>
        {{ item.name }}
      </span>
      <button class="h-full w-40 bg-slate-400 mr-2" @click="taskDelete(item)">删除</button>
    </div>
    <div class="grid m-10 p-2 grid-flow-row  grid-rows-1 grid-cols-2 gap-1 bg-gradient-to-br rounded-xl from-pink-300 to-rose-300">
      <input type="text" class="p-1" :value="newjob" @input="handleInput" />
      <button class="inline-block w-20 bg-slate-600 h-10 rounded-sm text-white" @click="addJob">添加</button>
    </div>
  </main>
</template>

