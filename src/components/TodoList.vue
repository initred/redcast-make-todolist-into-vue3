<template>
  <div class="max-w-xl max-h-96 w-full h-full">
    <div class="bg-gray-50 border border-gray-200 rounded shadow-lg divide-y divide-gray-200">
      <div class="bg-indigo-500 text-white p-4 rounded-tl rounded-tr">
        <h1 class="text-xl italic">Todo List</h1>
      </div>
      <div class="flex flex-col p-4">
        <div class="flex space-x-2">
          <div class="flex-1">
            <input
              class="w-full rounded-sm border-gray-300 text-sm"
              type="text" 
              id="todo-input"
              placeholder="add items"
            />
          </div>
          <button
            class="bg-indigo-500 rounded-sm text-white text-sm px-4"
            type="button"
            @click="add"
          >
            추가
          </button>
        </div>
      </div>
      <div 
        v-if="items.length > 0"
        class="flex flex-col space-y-2 p-4"
      >
        <div
          class="flex items-center justify-between bg-white border border-gray-200 rounded-lg p-3 overflow-hidden"
          v-for="(item, index) in items"
          :key="index"
        >
          <p class="flex-1 overflow-hidden break-words">{{ item }}</p>
          <button
            class="bg-red-500 rounded-sm text-white py-2 px-4 text-sm ml-4" type="button" @click="remove"
          >
            삭제
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    const items = ref([]);

    function add() {
      console.log("add");

      const todoText = document.getElementById("todo-input").value;

      items.value.push(todoText);
    }

    function remove(itemsIndex) {
      console.log("remove");

      items.value.splice(itemsIndex, 1);
    }

    return {
      items,
      add,
      remove,
    }
  }
})
</script>