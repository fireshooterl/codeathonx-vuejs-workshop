<template>
  <div id="app">
    <section class="todoapp">
      <header class="header">
        <h1>{{ title }}</h1>
        <input class="new-todo" placeholder="What needs to be done?" autofocus>
      </header>
    </section>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      title: "Hello Vue!"
    };
  }
};
</script>

<style>
</style>
