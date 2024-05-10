<script setup>
const emit = defineEmits(["removeTodo"]);

defineProps({
  todosSort: Array,
});
</script>

<template>
  <section class="todo-list">
    <h3>TODO LIST</h3>
    <div class="list">
      <div
        v-for="todo in todosSort"
        v-bind:key="todo.id"
        :class="`todo-item ${todo.done && 'done'}`"
      >
        <label>
          <input type="checkbox" v-model="todo.done" />
          <span :class="`bubble ${todo.category}`"></span>
        </label>
        <div class="todo-content">
          <input type="text" v-model="todo.content" />
        </div>
        <div class="actions">
          <button class="delete" @click="emit('removeTodo', todo)">
            Delete
          </button>
        </div>
      </div>
    </div>
  </section>
</template>
