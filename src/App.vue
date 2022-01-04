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

<template>
  <div class="todo-list">
    <h1 class="todo-list-h1">Todo List</h1>
    <div class="todo-list-add">
      <input type="text" id="todo-input" placeholder="add items" />
      <button type="button" @click="add">추가</button>
    </div>
    <div class="todo-items">
      <div v-for="(item, index) in items" :key="index">
        <div>{{ index + 1 }} - {{ item }}</div>
        <button type="button" @click="remove">삭제</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
html,
body,
#app {
  width: 100%;
  height: 100%;
  margin: 0px;
  padding: 0px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.todo-list {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.todo-list .todo-list-h1 {
  font-size: 24px;
}

.todo-list .todo-list-add {
  display: flex;
}

.todo-list .todo-items {
  margin-top: 8px;
  display: flex;
  flex-direction: column;
}

.todo-list .todo-items > * {
  display: flex;
  justify-content: space-between;
}
</style>
