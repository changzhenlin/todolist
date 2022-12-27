<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
    <div class="grid grid-flow-col grid-rows-2 grid-cols-3 gap-4 ">
      <div class="bg-slate-500 h-14">
        1
      </div>
      <div class="col-start-3 h-18 bg-pink-300">
        2
      </div>
      <div>
        3
      </div>
      <div>
        4
      </div>
      <div class="row-start-1 col-start-2 col-span-2 bg-gray-400 h-10">
        6
      </div>
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

