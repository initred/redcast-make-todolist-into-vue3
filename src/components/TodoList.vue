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
              v-model.trim="todoListText"
            />
          </div>
          <button
            class="bg-indigo-500 rounded-sm text-white text-sm px-4"
            type="button"
            @click="todoListAdd"
          >
            추가
          </button>
        </div>
      </div>
      <div class="max-h-80 overflow-y-auto">
        <div 
          v-if="todoListItems.length > 0"
          class="flex flex-col space-y-2 p-4"
        >
          <div
            class="flex items-center justify-between bg-white border border-gray-200 rounded-lg p-3 overflow-hidden"
            v-for="(item, index) in todoListItems"
            :key="index"
          >
            <div class="flex-1 flex items-center">
              <div class="mr-2.5">
                <input 
                  type="checkbox" 
                  class="rounded w-5 h-5 text-indigo-500"
                  :checked="item.isCompleted"
                  @input="(event) => todoListToggleCheck(event, index)"
                > 
              </div>
              <p :class="['flex-1', { 'line-through' :item.isCompleted }]">{{ item.text }}</p>
            </div>
            
            <button
              class="bg-red-500 rounded-sm text-white py-2 px-4 text-sm ml-4" 
              type="button" 
              @click="todoListRemove(index)"
            >
              삭제
            </button>
          </div>
        </div>
        <div
        v-else
        class="text-center py-12 bg-white text-sm text-gray-500"
        >
          할 일이 없습니다.
          <br>
          할 일을 추가해보세요.
        </div>
      </div>
      <div class="flex items-center justify-between p-4">
        <div class="bg-gray-500 text-white rounded text-sm">
          <div class="py-2 px-4">
          {{ todoListCompletedItemsLength }} / {{ todoListItems.length }}
          </div>
        </div>
        <button 
          type="button" 
          class="bg-red-500 rounded-sm text-white py-2 px-4 text-sm ml-4"
          @click="todoListCompletedItemsRemove"
        >
          완료된 할 일 모두 삭제
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, defineComponent, onBeforeMount, onMounted, ref } from "vue";

export default defineComponent({
  setup() {
    const todoListText = ref('')
    const todoListItems = ref([]);
    const todoListCompletedItemsLength = computed(() => 
      todoListItems.value.filter((item) => item.isCompleted).length
    )
    const todoListDefaultItemOptions = {
      isCompleted: false,
      isEdited: false,
    }

    function todoListAdd() {
      if(todoListText.value) {
        todoListItems.value.push({
          text: todoListText.value,
          ...todoListDefaultItemOptions,
        });
        localStorage.setItem('TodoList', JSON.stringify(todoListItems.value))
        todoListText.value = ''
      }
    }
    
    function todoListRemove(index) {
      todoListItems.value.splice(index, 1);
      localStorage.setItem('TodoList', JSON.stringify(todoListItems.value))
    }

    function todoListToggleCheck(event, index) {
      todoListItems.value[index].isCompleted = event.target.checked
    }

    function todoListCompletedItemsRemove() {      
      todoListItems.value = todoListItems.value.filter((item) => !item.isCompleted)
    }

    onBeforeMount(() => {
      if(localStorage.getItem('TodoList')) {
        todoListItems.value = JSON.parse(localStorage.getItem('TodoList'))
      }
    })

    return {
      todoListText,
      todoListItems,
      todoListCompletedItemsLength,
      todoListAdd,
      todoListRemove,
      todoListToggleCheck,
      todoListCompletedItemsRemove,
    }
  }
})
</script>
