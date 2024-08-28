<!-- src/components/TodoList.vue -->
<template>
  <div>
    <div class="flex mb-4">
      <input
        v-model="newTask"
        type="text"
        class="flex-grow p-2 border border-gray-300 rounded"
        placeholder="Tambahkan tugas baru..."
        @keyup.enter="addTask"
      />
      <button
        @click="addTask"
        class="ml-2 bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600"
      >
        Tambah
      </button>
    </div>

    <ul class="space-y-2">
      <li
        v-for="(task, index) in tasks"
        :key="index"
        class="flex items-center justify-between p-2 border rounded"
        :class="{ 'bg-green-100': task.completed }"
      >
        <span :class="{ 'line-through': task.completed }">{{ task.name }}</span>
        <div>
          <button
            @click="toggleComplete(index)"
            class="bg-yellow-400 text-white px-2 py-1 rounded hover:bg-yellow-500 mr-2"
          >
            {{ task.completed ? "Undo" : "Selesai" }}
          </button>
          <button
            @click="removeTask(index)"
            class="bg-red-500 text-white px-2 py-1 rounded hover:bg-red-600"
          >
            Hapus
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

// State
const tasks = ref([]);
const newTask = ref("");

// Functions
const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ name: newTask.value, completed: false });
    newTask.value = "";
  }
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const toggleComplete = (index) => {
  tasks.value[index].completed = !tasks.value[index].completed;
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
