<script setup lang="ts">
import { ref, watch, onMounted } from "vue";

const name = ref("");

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
  </main>
</template>
