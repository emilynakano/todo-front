<script setup lang="ts">
import { ref, watch, onMounted } from "vue";

const name = ref("");
const input_category = ref(null);
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
      <form>
        <h4>What's on in your todo list?</h4>
        <input type="text" placeholder="e.g. make a video" />
        <h4>Pick your category</h4>
        <div class="options">
          <label>
            <input type="radio" value="personal" v-model="input_category" />
            <span class="bubble personal"></span>
            <div>personal</div>
          </label>

          <label>
            <input type="radio" value="business" v-model="input_category" />
            <span class="bubble business"></span>
            <div>business</div>
          </label>
        </div>
      </form>
    </section>
  </main>
</template>
