<script setup>
import { ref } from "vue";

const name = ref("Fraz");
const isActive = ref(true);
const tasks = ref(["Task One", "Task Two"]);
const newTask = ref("");
const isEditing = ref(false);
const editIndex = ref(null);

const addTask = () => {
  if (!isActive.value) {
    alert("User needs to be active to add a new task");
    return;
  }
  if (newTask.value) {
    if (tasks.value.includes(newTask.value)) {
      alert("Task already exists");
    } else {
      tasks.value.push(newTask.value);
    }
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

const editTask = (index) => {
  isEditing.value = true;
  editIndex.value = index;
  newTask.value = tasks.value[index];
};

const updateTask = () => {
  if (newTask.value) {
    if (tasks.value.includes(newTask.value) && editIndex.value !== tasks.value.indexOf(newTask.value)) {
      alert("Task already exists");
    } else {
      tasks.value[editIndex.value] = newTask.value;
      newTask.value = "";
      isEditing.value = false;
      editIndex.value = null;
    }
  }
};

const cancelEdit = () => {
  isEditing.value = false;
  newTask.value = "";
  editIndex.value = null;
};

const toggleActive = () => {
  isActive.value = !isActive.value;
};
</script>

<template>
  <div class="app">
    <h1>{{ name }}</h1>
    <p :class="{ active: isActive, inactive: !isActive }">
      {{ name }} is {{ isActive ? "active" : "not active" }}
    </p>

    <form @submit.prevent="isEditing ? updateTask() : addTask()" class="task-form">
      <label for="newTask">{{ isEditing ? "Update Task" : "Add Task" }}</label>
      <input
        v-model="newTask"
        type="text"
        id="newTask"
        placeholder="Enter a task"
      />
      <button :disabled="!newTask" type="submit">
        {{ isEditing ? "Update" : "Add" }}
      </button>
      <button v-if="isEditing" @click.prevent="cancelEdit" type="button" class="cancel-btn">
        Cancel
      </button>
    </form>

    <h3>Tasks</h3>
    <ul class="task-list">
      <li v-for="(t, index) in tasks" :key="index">
        <span>{{ t }}</span>
        <button @click="editTask(index)" class="update-btn">Edit</button>
        <button @click="deleteTask(index)" class="delete-btn">Delete</button>
      </li>
    </ul>

    <button class="toggle-button" @click="toggleActive">Change Status</button>
  </div>
</template>

<style scoped>
.app {
  font-family: Arial, sans-serif;
  max-width: 400px;
  margin: 2rem auto;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

h1 {
  text-align: center;
  color: #333;
}

h3 {
  margin-top: 1.5rem;
  color: #555;
}

p {
  text-align: center;
  font-weight: bold;
  margin-bottom: 1rem;
}
.active {
  color: green;
}
.inactive {
  color: red;
}

.task-form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.task-form label {
  font-weight: bold;
}

.task-form input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.task-form button {
  padding: 0.5rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s;
}

.task-form button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.task-form button:not(:disabled):hover {
  background-color: #0056b3;
}

.cancel-btn {
  background-color: #6c757d;
  color: white;
}

.cancel-btn:hover {
  background-color: #5a6268;
}

.task-list {
  list-style-type: none;
  padding: 0;
  margin-top: 1rem;
}

.task-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  padding: 0.5rem;
  margin-bottom: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.task-list span {
  flex-grow: 1;
}

.update-btn {
  margin-right: 0.5rem;
  padding: 0.4rem;
  background-color: #ffc107;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.update-btn:hover {
  background-color: #e0a800;
}

.delete-btn {
  padding: 0.4rem;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.delete-btn:hover {
  background-color: #c82333;
}

.toggle-button {
  display: block;
  width: 100%;
  margin-top: 1.5rem;
  padding: 0.5rem;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
}

.toggle-button:hover {
  background-color: #218838;
}
</style>
