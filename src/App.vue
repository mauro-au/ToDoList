<template>
  <div class="todolist">
    <div class="todolist__main">
      <div class="container">
        <title>
          <h1>{{ message }}</h1>
        </title>
        <br />
        <form class="todolist__search">
          <input type="text" id="input" placeholder="Ingrese una nueva tarea" v-model="task" @keyup.enter.prevent="saveToDo"/>
          <button class="btn btn-primary" @click.prevent="saveToDo">Crear</button>
        </form>
        <ul class="container">
            <li v-for="(tarea, index) in toDoList" :key="index">
              <input type="checkbox">{{index}}:{{tarea.name}}
              <span class="btn btn-danger" @click="delateToDo(index)">X</span>
            </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      message: "Crear una nueva tarea",
      task: "",
      toDoList: [],
    };
  },
  methods: {
    saveToDo() {
      if (this.task !== "") {
        this.toDoList.push({ name: this.task, done: false });
        this.show = true
      }
      this.task = "";
    },
    delateToDo(index) {
      if (this.toDoList.length == 1) {
        this.show = false
      }
      this.toDoList.splice(index, 1);
    },
  }
};
</script>
<style scoped>
.todolist {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  height: 100vh;
}
.todolist__main {
  color: #415c79;
  text-align: center;
  background: #fff;
  border-radius: 20px;
  padding: 50px;
  animation-name: opacity;
  animation-duration: 1.5s;
  box-shadow: 0 2px 43px -4px rgba(0, 0, 0, 0.19) !important;
}
.todolist__search {
    -webkit-box-align: center;
    align-items: center;
    background: #f1f1f1;
    border-radius: 10px;
    border: 2px solid #ffffff;
    display: -webkit-box;
    display: flex;
    -webkit-box-pack: justify;
    justify-content: space-between;
    margin: 0.5em 0;
    padding: 0.5em 0.5em 0.5em 1em;
    transition: all 0.5s;
    -webkit-transition: all 0.5s;
    width: 450px
}
.todolist__search:hover,
.todolist__search:focus {
    border: 2px solid #e6e6e6;
}

.todolist__search button,
.todolist__search input {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;    
    border: 0;
    color: inherit;
    font-size: 1.5rem;
    outline: 0
}
.todolist__search button {
    cursor: pointer;
    padding: 0.2em 0.8em;
    border-radius: 10px;
    color: #fff;
    font-size: 1.3rem;
}
.todolist__search input {
    -webkit-box-flex: 1;
    flex: 1;
    background: transparent;
    font-weight: 500;
    font-size: 23px
}

.todolist__search input::placeholder {
    color: #c2c2c2
}
</style>