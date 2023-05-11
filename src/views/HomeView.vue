<template>
  <h1>Nurul Fadhila - To Do List</h1>
  <div>
    <input v-model="newTodo" placeholder="Kegiatan">
    <button @click="addTodo">Tambah</button>
    <br><br>
    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Tampilkan Semua' : 'Sembunyikan yang sudah selesai' }}</button>
    <ul>
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
        <button v-if="!todo.completed" @click="completeTodo(todo.id)">Selesai</button>
        <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">Belum Selesai</button>
        <button @click="removeTodo(todo.id)">Hapus</button>
      </li>
    </ul>
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
body {
  background-color: #827979;
}

h1{
  color: white;
}

ul li{
  list-style-type: none;
  padding: 12px 8px 12px 50px;
  font-size: 17px;
  user-select: none;
  cursor: pointer;
  margin: 0;
  position: relative;
  color: white;
}
.completed {
  text-decoration: line-through;
}
button {
  margin-left: 10px;
  padding: 8px;
    font-size: 12px;
    border-radius: 4px;
    border: none;
    background-color: #686883;
    color: white;
    cursor: pointer;
    margin-top: 10px;
}
</style>