<script>
import { defineComponent } from "vue";
import TodoList from "./components/TodoList.vue";

export default defineComponent({
  components: {
    TodoList,
  }
})
</script>

<template>
  <div class="w-full h-full flex justify-center items-center">
    <todo-list />
  </div>
</template>