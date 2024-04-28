<template>
  <h1>To Do List</h1>
  <div class="todo-container">
    <input v-model="newTodo" placeholder="Masukkan Kegiatan">
    <button @click="addTodo">Tambah Kegiatan</button>
    <br><br>
    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Tampilkan Semua' : 'Sembunyikan yang sudah selesai' }}</button>
    <table>
      <thead>
        <tr>
          <th>Kegiatan</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in visibleTodos" :key="todo.id">
          <td>
            <span :class="{ completed: todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
          </td>
          <td>
            <div class="action-buttons">
              <button v-if="!todo.completed" @click="completeTodo(todo.id)" class="complete-btn">Selesai</button>
              <button v-if="todo.completed" @click="unCompleteTodo(todo.id)" class="incomplete-btn">Belum Selesai</button>
              <button @click="removeTodo(todo.id)" class="delete-btn">Hapus</button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>





<script>
export default {
name: 'App',
data() {
return {
  todos: [],
  newTodo: '',
  nextId: 1,
  hideCompleted: false
}
},
computed: {
visibleTodos() {
  if (this.hideCompleted) {
    return this.todos.filter(todo => !todo.completed);
  } else {
    return this.todos;
  }
}
},
methods: {
addTodo() {
  if (this.newTodo.trim() !== '') {
    this.todos.push({
      id: this.nextId++,
      text: this.newTodo,
      completed: false
    });
    this.newTodo = '';
  }
},
removeTodo(id) {
  this.todos = this.todos.filter(todo => todo.id !== id);
},
completeTodo(id) {
  const todo = this.todos.find(todo => todo.id === id);
  if (todo) {
    todo.completed = true;
  }
},
unCompleteTodo(id) {
  const todo = this.todos.find(todo => todo.id === id);
  if (todo) {
    todo.completed = false;
  }
},
toggleComplete(todo) {
  todo.completed = !todo.completed;
}
}
}
</script>

<style>
Body {
  color: #274665;
  background-image: url(/src/assets/dark.jpeg); 
  background: cover;
background-size: cover;
background-repeat: no-repeat
}
.todo-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  border-radius: 10px;
  background-color: #13252a; /* Darker background color */
  color: #6f3a3a; /* White text for better contrast */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  margin-bottom: 20px;
  font-size: 2em;
  font-weight: bold;
  text-align: center;
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  background-color: #3a3a3a; /* Darker input field */
  color: #fff; /* White text for input field */
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  margin: 5px;
  background-color: #3a3a3a; /* Darker button background */
  color: #fff; /* White text for buttons */
}

.complete-btn {
  background-color: #4CAF50; /* Green for completed button (unchanged) */
  color: white;
}

.incomplete-btn {
  background-color: #f44336; /* Red for incomplete button (unchanged) */
  color: white;
}

.delete-btn {
  background-color: #e04444; /* Red for delete button */
  color: white;
}

ul {
  list-style: none;
  padding: 0;
  width: 100%;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  background-color: #454d55; /* Darker background for todo items */
  color: #fff; /* White text for todo items */
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
  color: #aaa; /* Lighter grey for completed text */
}

.action-buttons {
  display: flex;
}

.action-buttons button {
  margin-left: 5px;
}

</style>