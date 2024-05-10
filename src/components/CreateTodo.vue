<script setup>
import { ref } from "vue";

const emit = defineEmits(["addTodo"]);

const inputContent = ref("");
const inputCategory = ref(null);

const handleSubmit = () => {
  if (inputContent.value.trim() === "" || inputCategory.value === null) {
    return;
  }

  emit("addTodo", inputContent.value, inputCategory.value);

  inputContent.value = "";
  inputCategory.value = null;
};
</script>

<template>
  <section class="create-todo">
    <h3>CREATE A TODO</h3>
    <form @submit.prevent="handleSubmit">
      <h4>What's on your todo list?</h4>
      <input
        type="text"
        placeholder="do something nice"
        v-model="inputContent"
      />
      <h4>Pick a category</h4>
      <div class="options">
        <label>
          <input
            type="radio"
            name="category"
            value="business"
            v-model="inputCategory"
          />
          <span class="bubble business"></span>
          <div>business</div>
        </label>

        <label>
          <input
            type="radio"
            name="category"
            value="personal"
            v-model="inputCategory"
          />
          <span class="bubble personal"></span>
          <div>personal</div>
        </label>
      </div>

      <input type="submit" value="Add todo" />
    </form>
  </section>
</template>
