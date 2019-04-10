<template>
  <div id="app">
    <section class="todoapp">
      <header class="header">
        <h1>{{ title }}</h1>
      </header>
      <input
        class="new-todo"
        placeholder="What needs to be done?"
        v-on:keyup.enter="createTodo"
        autofocus
      >
      <section class="main">
        <ul class="todo-list">
          <li
            v-for="todo in todos"
            :key="todo.text"
            :class="{ completed: todo.isDone, editing: todo === editing }"
          >
            <div class="view">
              <input class="toggle" type="checkbox" v-model="todo.isDone">
              <label @dblclick="startEditing(todo)">{{todo.text}}</label>
              <button class="destroy" @click="destroyTodo(todo)"></button>
            </div>
            <input
              class="edit"
              @keyup.esc="cancelEditing"
              @keyup.enter="finishEditing"
              @blur="finishEditing"
              :value="todo.text"
            >
          </li>
        </ul>
      </section>
      <footer class="footer">
        <span class="todo-count">
          <strong>{{activeTodos.length}}</strong> item(s) left
        </span>
      </footer>
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
      <p>Esc to cancel edit</p>
      <p>Enter to accept edit</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      title: "Hello Vue!",
      todos: [
        { text: "Learn JavaScript ES6+ goodies", isDone: true },
        { text: "Learn Vue", isDone: false },
        { text: "Build something awesome", isDone: false }
      ],
      editing: null
    };
  },
  computed: {
    activeTodos() {
      return this.todos.filter(t => !t.isDone);
    }
  },
  methods: {
    createTodo(event) {
      const textbox = event.target;
      this.todos.push({ text: textbox.value, isDone: false });
      textbox.value = "";
    },
    startEditing(todo) {
      this.editing = todo;
    },
    finishEditing(event) {
      if (!this.editing) {
        return;
      }
      const textbox = event.target;
      this.editing.text = textbox.value;
      this.editing = null;
    },
    cancelEditing() {
      this.editing = null;
    },
    destroyTodo(todo) {
      const index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style>
</style>
