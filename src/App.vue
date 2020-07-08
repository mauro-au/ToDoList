<template>
  <div class="todolist">
    <div class="todolist__main">
      <div class="container">
        <section class="title">
          <h1>{{ message }}</h1>
        </section>
        <br />
        <form class="todolist__search">
          <input type="text" id="input" placeholder="Ingrese una nueva tarea" v-model="task" @keyup.enter.prevent="saveToDo"/>
          <button class="btn btn-primary" @click.prevent="saveToDo">Crear</button>
        </form>
        <section class="todolist__card">
          <ul class="my-4">
            <li v-for="(toDo, index) in toDoList" :key="index">
              <div class="card" :class="{ card__taskdone: toDo.done }">
                <div class="card-body">
                  <div class="card__left">
                    <input type="checkbox" v-model="toDo.done"/>
                    <span class="card__line">{{ toDo.name }}</span>
                  </div>
                  <span class="btn btn-danger" @click="delateToDo(index)">X</span>
                </div>
              </div>
            </li>
          </ul>
          <button class="btn btn-primary btn-lg btn-block mt-5 card__delate" v-if="show" @click="allDelateToDo">Borrar todo</button>
        </section>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      message: "Lista de Tareas",
      task: "",
      toDoList: [],
      show: false
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
    allDelateToDo() {
      this.show = false
      this.toDoList = [];
    }
  },
}
</script>

<style land>

@keyframes opacity{
  0% {
    opacity:0;
    margin-top: -25px;
  }
  100% {
    position: relative;
    opacity: 1;
    margin-top: 0px;
  }
}
body{
  background: #d6d6d6 !important;

}
h1{
  font-weight: 900 !important;
}
li{
  list-style: none;
}
ul{
  padding-left: 0;
}
.todolist {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  height: 100vh;
}
.todolist__counter{
  font-size: 1.3rem;
  color: #bfbfbf
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
.card {
  transition: all 0.2s ease-out !important;
  box-shadow: 0 2px 20px -4px rgba(0, 0, 0, 0.19) !important;
  margin-bottom: 1.2rem;
  border-radius: 10px !important;
  position: absolute;
  border: none !important;
  animation-name: opacity;
  animation-duration: 1s;
}
.card:hover {
  transform: translateY(2px);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.05) !important;
}
.card-body{
  justify-content: space-between;
  display: flex;
  align-items: center;
  padding: 1rem 1.5rem!important;
  border-radius: 15px;
}
.card__delate{
  animation-name: opacity;
  animation-duration: 1.2s;
}
.card__line{
  margin-left: 15px;
  font-size: 1.5rem;
}
.card__taskdone{
  opacity: .5;
  transform: translateY(2px);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.05) 
}
.card__taskdone .card__line {
  text-decoration: line-through;
}
</style>