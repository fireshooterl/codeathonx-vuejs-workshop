<template>
  <div id="app">
    <section class="todoapp">
      <header class="header">
        <h1>{{ title }}</h1>
        <input class="new-todo" placeholder="What needs to be done?" autofocus>
      </header>
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
  }
};
</script>

<style>
</style>
