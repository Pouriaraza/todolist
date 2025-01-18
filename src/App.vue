<script setup>
import { ref, onMounted, computed, watch } from "vue";

const todos = ref([]);
const name = ref("");

const input_content = ref("");
const input_category = ref(null);

const todos_asc = computed(() =>
  todos.value.sort((a, b) => {
    return a, createdAt - b.createdAt;
  })
);

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  {
    deep: true,
  }
);

// const addTodo = () => {
//   if (input_content.value.trim() === "" || input_category.value === null) {
//     return;
//   }

//   todos.value.push({
//     content: input_content.value,
//     category: input_category.value,
//     done: false,
//     editable: false,
//     createdAt: new Date().getTime(),
//   });
// };

// const removeTodo = (todo) => {
//   todos.value = todos.value.filter((t) => t !== todo);
// };

// onMounted(() => {
//   name.value = localStorage.getItem("name") || "";
//   todos.value = JSON.parse(localStorage.getItem("todos")) || [];
// });
</script>

<template>
  <main class="app">
    <section class="todo">
      <h2 class="title">
        What's up,
        <input type="text" id="name" placeholder="Name Here" v-model="name" />
      </h2>
    </section>

    <section class="creat-todo">
      <h3>CREATE A TODO</h3>

      <form @submit.prevent="" addTodo>
        <h4>What's on your todo List?</h4>
        <input
          type="text"
          name="content"
          placeholder="e.g. Make a video"
          v-model="input_category"
        />

        <h4>Pick a category</h4>
        <div class="options">
          <label>
            <input type="radio" name="category" v-model="input_category" />
            <div>Bussiness</div>
          </label>

          <label>
            <input type="radio" name="category" v-model="input_category" />
            <div>personal</div>
          </label>
        </div>
      </form>
    </section>
  </main>
</template>
