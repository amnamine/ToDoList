<template>
  <div id="app" class="bg-gradient-to-r from-blue-400 to-purple-600 min-h-screen flex flex-col items-center justify-center p-5">
    <h1 class="text-4xl font-bold text-white mb-5">Todo List</h1>
    <div class="todo-container flex mb-4">
      <input
        type="text"
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Add a new task"
        class="todo-input w-3/4 p-2 rounded-l-lg border border-gray-300 focus:outline-none focus:border-blue-500 transition"
      />
      <button @click="addTodo" class="add-button bg-blue-500 text-white rounded-r-lg px-4 hover:bg-blue-600 transition">Add</button>
    </div>
    <transition-group name="fade" tag="ul" class="w-full max-w-md">
      <li
        v-for="(todo, index) in todos"
        :key="todo.id"
        class="todo-item bg-white shadow-md rounded-lg flex items-center justify-between p-3 mb-2 transition-transform transform hover:scale-105"
      >
        <div class="flex items-center">
          <input
            type="checkbox"
            v-model="todo.completed"
            class="checkbox mr-3"
          />
          <span :class="{ 'line-through text-gray-400': todo.completed, 'text-gray-800': !todo.completed }" class="text-lg">{{ todo.text }}</span>
        </div>
        <button @click="removeTodo(index)" class="remove-button bg-red-500 text-white rounded-lg px-3 hover:bg-red-600 transition">Remove</button>
      </li>
    </transition-group>
    <p v-if="todos.length === 0" class="no-todos text-white">No tasks yet!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') return;
      this.todos.push({ id: Date.now(), text: this.newTodo, completed: false });
      this.newTodo = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
/* Animation */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
