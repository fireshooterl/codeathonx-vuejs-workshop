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
      <ul class="todo-list">
        <li
          v-for="todo in todos"
          :key="todo.text"
          :class="{ completed: todo.isDone, editing: todo === editing }"
        >
          <div class="view">
            <input class="toggle" type="checkbox" v-model="todo.isDone">
            <label @dblclick="startEditing(todo)">{{todo.text}}</label>
            <button class="destroy"></button>
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
    }
  }
};
</script>

<style>
</style>
