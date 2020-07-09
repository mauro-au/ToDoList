<template>
  <div id="app">
    <ToDoList/>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue'

export default {
  name: 'App',
  components: {
    ToDoList
  }
}
</script>

<style lang="scss">
body{
  background: #d6d6d6 !important;
}
</style>
