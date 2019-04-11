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
          <TodoItem
            v-for="todo in todos"
            :key="todo.text"
            :todo="todo"
            :editing="editing"
            @start-edit="startEditing"
            @finish-edit="finishEditing"
            @cancel-edit="cancelEditing"
            @destroy-todo="destroyTodo"
          ></TodoItem>
        </ul>
      </section>
      <footer class="footer">
        <span class="todo-count">
          <strong>{{activeTodos.length}}</strong> item(s) left
        </span>
        <button
          class="clear-completed"
          @click="clearCompleted"
          v-show="completedTodos.length"
        >Clear completed</button>
      </footer>
    </section>
    <Footer></Footer>
  </div>
</template>

<script>
import Footer from "./components/Footer";
import TodoItem from "./components/TodoItem";

export default {
  name: "App",
  components: {
    Footer,
    TodoItem
  },
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
    },
    completedTodos() {
      return this.todos.filter(t => t.isDone);
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
      console.log(this.editing);
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
    },
    clearCompleted() {
      this.todos = this.activeTodos;
    }
  }
};
</script>

<style>
</style>
