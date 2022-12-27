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
  <header class="bg-pink-200">
    <div class="grid m-10 p-2 grid-flow-col grid-rows-2 grid-cols-3 gap-4 bg-gradient-to-br rounded-2xl from-pink-300 to-rose-300">
      <input type="text" :value="newjob" @input="handleInput" />
      <button @click="addJob">添加</button>
    </div>
  </header>

  <main class="bg-gray-200">
    <div v-for="item in itemList" class="grid m-10 p-2 grid-flow-col grid-rows-2 grid-cols-3 gap-4 bg-gradient-to-br rounded-2xl from-pink-300 to-rose-300">
      {{ item.name }}
    </div>
  </main>
</template>

