<script setup lang="ts">
import { ref, watch, onMounted, type Ref } from "vue";

type Category = "personal" | "business" | "";

interface ITodo {
  content: string;
  category: Category;
  done: boolean;
}

const name = ref("");
const todo_category: Ref<Category> = ref("");
const todo_name: Ref<string> = ref("");
const todos: Ref<ITodo[]> = ref([]);

function addTodo() {
  todos.value.push({
    content: todo_name.value,
    category: todo_category.value,
    done: false,
  });
  todo_name.value = "";
  todo_category.value = "";
}
const Submit = () => {};

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
});
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        What's up <input type="text" placeholder="Your name" v-model="name" />
      </h2>
    </section>
    <section class="create-todo">
      <h3>CREATE A TODO</h3>
      <form @submit="addTodo" @submit.prevent="Submit">
        <h4>What's on in your todo list?</h4>
        <input
          type="text"
          placeholder="e.g. make a video"
          v-model="todo_name"
        />
        <h4>Pick your category</h4>
        <div class="options">
          <label>
            <input type="radio" value="personal" v-model="todo_category" />
            <span class="bubble personal"></span>
            <div>personal</div>
          </label>

          <label>
            <input type="radio" value="business" v-model="todo_category" />
            <span class="bubble business"></span>
            <div>business</div>
          </label>
        </div>
        <input type="submit" value="Add todo" />
      </form>
    </section>
    <section class="todo-list">
      <h3>TODO LIST</h3>
      <div class="list">
        <div
          v-for="todo in todos"
          :key="todo.content"
          :class="`todo-item ${todo.done && 'done'}`"
        >
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span :class="`bubble ${todo.category}`"></span>
          </label>
          <div class="todo-content">
            {{ todo.content }}
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
