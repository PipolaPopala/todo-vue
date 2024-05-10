<script setup>
import { ref, onMounted, computed, watch } from "vue";
import Greeting from "./components/Greeting.vue";
import CreateTodo from "./components/CreateTodo.vue";
import TodoList from "./components/TodoList.vue";

const todos = ref([]);

const todosSort = computed(() =>
  todos.value.sort((a, b) => b.createdAt - a.createdAt)
);

const addTodo = (inputContent, inputCategory) => {
  todos.value.push({
    content: inputContent,
    category: inputCategory,
    done: false,
    createdAt: new Date().getTime(),
  });
};

const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  {
    deep: true,
  }
);

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});
</script>

<template>
  <main class="app">
    <Greeting />

    <CreateTodo @add-todo="addTodo" />

    <TodoList :todosSort="todosSort" @remove-todo="removeTodo" />
  </main>
</template>
