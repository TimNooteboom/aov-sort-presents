<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>
      <div class="mt-2 flex justify-center items-center">
        <img
          v-for="present in presentsSorted"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <button class="bg-slate-900 hover:bg-slate-700 text-white font-semibold h-12 px-6 rounded-lg flex items-center justify-center mx-auto mt-8" @click="toggleSort">Toggle Sort</button>
    </div>
  </div>
</template>

<script setup>
  import presents from './presents.json'
  import { ref, computed } from 'vue'
  let smallSort = ref(false)

  const presentsSorted = computed(() => {
    if(smallSort.value) {
      return presents.sort((a, b) => {
        return a.dimensions.width - b.dimensions.width
      })
    } else {
      return presents.sort((a, b) => {
        return a.id - b.id
      })
    }
  })

  const toggleSort = () => {
    smallSort.value === true ? smallSort.value = false : smallSort.value = true 
  }

  // An interesting solution provided
  /*
  const sortFunctions = {
    smallToBig: (a, b) => a.dimensions.width * a.dimensions.height - b.dimensions.width * b.dimensions.height,
    default: (a, b) => a.id - b.id,
  }
  const sortFunctionActive = ref('default')
  const toggleSort = () => {
    sortFunctionActive.value = sortFunctionActive.value === 'default' ? 'smallToBig' : 'default'
  }
  const presentsSorted = computed(() => [...presents].sort(sortFunctions[sortFunctionActive.value]))
  */
</script>
