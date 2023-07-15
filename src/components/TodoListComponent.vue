<template>
  <div class="todoContainer">
    <h1>쀼로 만드는 Todo List</h1>
    <div class="inputBox">
      <input
        type="text"
        v-model="inputText"
        @keydown.enter="handleAdd"
        placeholder="할 일을 입력하세요"
      />
      <button @click="handleAdd">ADD</button>
    </div>
    <TodoList :todoitems="todoitems" @newTodoEmit="handleNewTodo" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import TodoList from "../components/TodoList.vue";

const inputText = ref("");
const todoitems = ref([]);
const todoId = ref(0);

const handleAdd = () => {
  if (inputText.value === "") {
    alert("할 일을 입력하세요!");
    return;
  }
  todoitems.value.push({
    id: todoId.value,
    item: inputText.value,
    state: false,
    editState: false,
  });
  inputText.value = "";
  todoId.value++;
};

const handleNewTodo = (newTodo) => {
  todoitems.value = newTodo;
};
</script>

<style scoped>
.todoContainer {
  width: 400px;
  height: 100vh;
  margin: 0 auto;
  text-align: center;
}

h1 {
  padding: 32px 0;
}

input {
  padding: 8px 16px;
  border-radius: 4px;
  margin-right: 8px;
}

button {
  padding: 9px 16px;
  border-radius: 4px;
  cursor: pointer;
  color: white;
  background-color: rgb(102, 175, 169);
  border: 1px solid black;
}

button:hover {
  background-color: rgb(122, 207, 200);
}

.inputBox {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
