<template>
  <div id="app">
    <div class="new-task-wrapper">
      <input data-testid="new-task-input" maxlength="50" class="new-task" v-model="newTask" placeholder="Wpisz nowe zadanie" />
      <button data-testid="new-task-button" class="add-btn" @click="addTask">Dodaj zadanie</button>
    </div>
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span :class="{ 'task-name': true, 'done': task.done }">{{ task.text }}</span>
        <div class="buttons-wrapper">
          <button :data-testid="`toggle-btn-${index}`" class="toggle-btn" @click="toggleTask(index)">{{ `Oznacz jako ${task.done ? "nie" : ""}wykonane` }}</button>
          <button :data-testid="`delete-btn-${index}`" class="delete-btn" @click="deleteTask(index)">Usuń</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'
import "./index.css"

export default {
  setup() {
    const newTask = ref('')
    const tasks = ref([])

    const addTask = () => {
      tasks.value.push({ text: newTask.value, done: false })
      newTask.value = ''
    }

    const deleteTask = index => {
      tasks.value.splice(index, 1)
    }

    const toggleTask = index => {
      tasks.value[index].done = !tasks.value[index].done
    }

    return { newTask, tasks, addTask, deleteTask, toggleTask }
  }
}
</script>

<style>
#app {
  width: 700px;
  margin: 0 auto;
}

.new-task {
  width: 100%;
  height: 30px;
  padding: 5px 10px;
  margin: 10px 10px 10px 0;
  border-radius: 10px;
  border: none;
  font-size: 16px;
  font-weight: bold;
  background-color: #34495e;
  color: #d1e8df;
  font-family : inherit;
}

.new-task::placeholder {
  color: #4c7474;
  font-weight: bold;
}

.add-btn, .toggle-btn, .delete-btn {
  font-family : inherit;
  width: 220px;
  height: 40px;
  border-radius: 10px;
  border: none;
  background-image: linear-gradient(to right, #41b883, #83a4a4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: bold;
  font-size: 16px;
}

.add-btn, .toggle-btn, .delete-btn:hover {
  cursor: pointer;
}

.delete-btn {
  -webkit-text-fill-color: red;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  margin: 10px 0;
  padding: 10px;
  background-color: #344c5c;
  display: flex;
  justify-content: space-between;
  border-radius: 10px;
}

.done {
  text-decoration: line-through;
  text-decoration-thickness: 2px;
}

.new-task-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task-name {
  line-height: 70px;
  padding: 0 10px;
  font-weight: bold;
  color: #d1e8df;
}

.buttons-wrapper {
  display: flex;
  flex-direction: column;
  row-gap: 10px;
}
</style>