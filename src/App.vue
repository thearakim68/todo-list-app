<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoList
  }
}
</script>

<style>
    * {
      box-sizing: border-box;
    }
    #app {
      font-family: Arial, Helvetica, sans-serif;
      text-align: center;
      color: #2c3e50;
      margin-top: 60px;
    }
</style>