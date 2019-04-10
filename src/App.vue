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
        <li v-for="todo in todos" :key="todo.text">
          <div class="view">
            <input class="toggle" type="checkbox">
            <label>{{todo.text}}</label>
            <button class="destroy"></button>
          </div>
          <input class="edit" value="Rule the web">
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
      ]
    };
  },
  methods: {
    createTodo(event) {
      const textbox = event.target;
      this.todos.push({ text: textbox.value, isDone: false });
      textbox.value = "";
    }
  }
};
</script>

<style>
</style>
