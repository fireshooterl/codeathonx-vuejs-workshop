<template>
  <li :class="{ completed: todo.isDone, editing: todo === editing }">
    <div class="view">
      <input class="toggle" type="checkbox" v-model="todo.isDone">
      <label @dblclick="startEditing()">{{todo.text}}</label>
      <button class="destroy" @click="destroyTodo()"></button>
    </div>
    <input
      class="edit"
      @keyup.esc="cancelEditing"
      @keyup.enter="finishEditing"
      @blur="finishEditing"
      :value="todo.text"
    >
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      text: "",
      isDone: false
    },
    editing: null
  },
  methods: {
    startEditing() {
      console.log(this.todo === this.editing)
      this.$emit('start-edit', this.todo);
    },
    finishEditing(event) {
      this.$emit('finish-edit', event);
    },
    cancelEditing() {
      this.$emit('cancel-edit');
    },
    destroyTodo(todo) {
      this.$emit('destroy-todo');
    }
  }
};
</script>

