<template>
  <main>
    <!-- The overlay -->
    <div v-if="isShow" class="absolute bg-black/60 w-full h-screen items-center justify-center flex ">
        <div class="w-[400px] h-[300px] bg-white flex flex-col items-center justify-center gap-2">
          <textarea v-model.trim="newNote" class="h-full p-2.5 w-full text-sm text-gray-90 border border-1" placeholder="Type your note here..."></textarea>
          <div @click="addNote" class="bg-blue-300 w-full flex justify-center items-center cursor-pointer">Add Note</div>
          
          <div @click="isShow=false" class="bg-red-300 w-full flex justify-center items-center cursor-pointer">Cancel</div>
        </div>
      </div>
    <div class="w-full h-full flex items-center justify-center">
  
      <!-- container -->
      <div class="mx-20 w-full h-auto mt-20">
        <!-- The header  -->
        <div class="flex justify-between">
          <p class="text-[50px] font-bold text-gray-700">Notes</p>
          <button @click="isShow=true, clearText" class="bg-gray-200 m-3 px-4 rounded-full">
            <span class="text-center text-[30px]">+</span>
          </button>
        </div>

        <!-- The container of note  -->
        <ul class="flex gap-4 mt-5 flex-wrap">
          <li
            v-for="note in notes" :key="note.id" 
            class="flex flex-col justify-between p-2 w-[200px] h-[250px] rounded-lg bg"
            :style="{backgroundColor: note.backgroundColor}"
          >
            <p class="text-base">{{ note.label }}</p>
            <p class="text-[13px]">{{ note.date.toLocaleDateString("en-US") }}</p>
          </li>

          
        </ul>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const isShow = ref(false)

const newNote = ref('')

const notes = ref([])

const addNote = () => {
  notes.value.push({
    id: notes.value.length+1, 
    label: newNote.value, 
    date: new Date(), 
    backgroundColor: getRandomColor()})
  isShow.value = false
  newNote.value = ''
}

const clearText = () => {
  newNote.value = ''
}

const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 +", 100%, 75%)"
}


</script>

<style scope>
body {
  background-color: aliceblue;
}
</style>
