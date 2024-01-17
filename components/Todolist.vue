<template>
    <div class="container mx-auto p-4">
      <h2 class="text-2xl font-bold mb-4">Task List</h2>
  
      <ul>
        <li v-for="task in tasks" :key="task.name" class="mb-2">
          {{ task.name }} - {{ task.time }} minutes
          <button @click="removeTask(task)" class="ml-2 bg-red-500 text-white px-2 py-1 rounded">Remove</button>
        </li>
      </ul>
  
      <button @click="openAddTaskPopup" class="mt-4 bg-blue-500 text-white px-4 py-2 rounded">Add Task</button>
  
      <div v-if="isAddTaskPopupOpen" class="fixed inset-0 flex items-center justify-center">
        <div class="bg-white p-8 max-w-md w-full rounded shadow-lg">
          <form @submit.prevent="addTask">
            <div class="mb-4">
              <label for="taskName" class="block text-sm font-medium text-gray-600">Task Name:</label>
              <input v-model="newTaskName" type="text" id="taskName" required
                     class="mt-1 p-2 w-full border rounded-md">
            </div>
  
            <div class="mb-4">
              <label for="taskTime" class="block text-sm font-medium text-gray-600">Time (minutes):</label>
              <input v-model.number="newTaskTime" type="number" id="taskTime" required
                     class="mt-1 p-2 w-full border rounded-md">
            </div>
  
            <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded">Add Task</button>
          </form>
          <button @click="closeAddTaskPopup" class="mt-2 bg-gray-300 text-gray-700 px-4 py-2 rounded">Close</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const tasks = ref([
    { name: 'Task 1', time: 60 },
    { name: 'Task 2', time: 75 },
    // Add more tasks as needed
  ]);
  
  const isAddTaskPopupOpen = ref(false);
  const newTaskName = ref('');
  const newTaskTime = ref(0);
  
  const openAddTaskPopup = () => {
    isAddTaskPopupOpen.value = true;
  };
  
  const closeAddTaskPopup = () => {
    isAddTaskPopupOpen.value = false;
  };
  
  const addTask = () => {
    if (newTaskName.value && newTaskTime.value > 0) {
      tasks.value.push({ name: newTaskName.value, time: newTaskTime.value });
      closeAddTaskPopup();
      // Clear input fields
      newTaskName.value = '';
      newTaskTime.value = 0;
    }
  };
  
  const removeTask = (taskToRemove) => {
    tasks.value = tasks.value.filter((task) => task !== taskToRemove);
  };
  </script>
  