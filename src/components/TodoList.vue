<template>
  <div class="todoListContainer">
    <div class="todoItem" v-for="todo in props.todoitems" :key="todo.id">
      <div>
        <input :id="todo.id" type="checkbox" @change="handleState(todo)" />
        <input
          v-if="todo.editState"
          v-model="todo.editText"
          type="text"
          class="editInput"
        />
        <label v-else :for="todo.id" :class="todo.state ? 'complete' : ''">{{
          todo.item
        }}</label>
      </div>
      <div>
        <div v-if="!todo.editState">
          <button
            @click="toggleEditState(todo)"
            :class="todo.editState ? 'whiteButton editActive' : 'whiteButton'"
          >
            {{ todo.editState ? "CANCEL" : "EDIT" }}
          </button>
          <button @click="handleDelete(todo)">DELETE</button>
        </div>
        <div v-else>
          <button @click="toggleEditState(todo)" class="whiteButton">
            CANCEL
          </button>
          <button @click="handleSave(todo)" class="editActive">SAVE</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  todoitems: {
    type: Array,
  },
});

const handleState = (todo) => {
  todo.state = !todo.state;
};

const toggleEditState = (todo) => {
  todo.editState = !todo.editState;
  if (todo.editState) {
    todo.editText = todo.item;
  }
};

const handleDelete = (todo) => {
  const index = props.todoitems.indexOf(todo);
  if (index !== -1) {
    props.todoitems.splice(index, 1);
  }
};

const handleSave = (todo) => {
  todo.item = todo.editText;
  toggleEditState(todo);
};
</script>

<style scoped>
.todoListContainer {
  height: 450px;
  background-color: rgb(29, 27, 27);
  margin-top: 32px;
  padding: 18px;
  overflow: auto;
}

/* 스크롤 바 스타일 */
.todoListContainer::-webkit-scrollbar {
  width: 8px;
}

.todoListContainer::-webkit-scrollbar-thumb {
  background-color: rgb(102, 175, 169);
  border-radius: 4px;
}

.todoListContainer::-webkit-scrollbar-track {
  background-color: inherit;
}

label {
  margin-left: 8px;
}

.todoItem {
  padding: 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

button {
  border-radius: 4px;
  border: none;
  cursor: pointer;
  color: white;
  padding: 3px 8px;
  background-color: rgb(202, 62, 62);
}

.whiteButton {
  border-radius: 4px;
  border: none;
  cursor: pointer;
  color: black;
  padding: 3px 8px;
  background-color: rgb(255, 255, 255);
  margin-right: 5px;
}

.editActive {
  color: white;
  background-color: rgb(40, 161, 218);
}

.complete {
  text-decoration-line: line-through;
}

input[type="checkbox"] {
  width: 11px;
  height: 11px;
}

.editInput {
  margin-left: 8px;
}
</style>
