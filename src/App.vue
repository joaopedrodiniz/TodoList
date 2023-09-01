<template>
  <ListTodo />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ListTodo from './components/ListTasks.vue';

export default defineComponent({
  name: 'App',
  components: {
    ListTodo,
  }
});
</script>

<style>

*{
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  text-align: center;
  color: #2c3e50;
  width: 100%;
}
body {
  background: #222222;;
}
</style>
