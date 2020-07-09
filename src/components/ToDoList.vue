<template>
  <div class="todolist container" :style="[itemCounter.length > 1 ? styleObject : {}]">
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
          <p class="todolist__counter">Quedan {{ itemCounter.length }} Items</p>
          <ul class="my-4">
            <li v-for="(toDo, index) in toDoList" :key="index">
              <div class="card" :class="{ card__taskdone: toDo.done }">
                <div class="card-body">
                  <div class="card__left">
                    <input type="checkbox" v-model="toDo.done"/>
                    <span class="card__line">{{ toDo.name }}</span>
                  </div>
                  <span class="btn" @click="delateToDo(index)">
                    <img src="/img/cross.svg" class="card__delate-list" alt="">
                  </span>
                </div>
              </div>
            </li>
          </ul>
          <button class="btn btn-primary btn-lg btn-block mt-5 card__delate" v-if="show" @click="allDelateToDo">
            Borrar todo
            <img src="/img/trash.svg" alt="">
          </button>
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
      show: false,
      styleObject: {
        padding:'50px 0',
        alignItems:'flex-start',
        height: '100%',
      }
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
  computed: {
    itemCounter: function () {
      return this.toDoList.filter(checkbox => checkbox.done == false);
    }
  },
}
</script>

<style lang="scss">

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
  height: 100vh;
  &__counter{
    font-size: 1.3rem;
    color: #bfbfbf
  }
  &__main {
    color: #415c79;
    text-align: center;
    background: #fff;
    border-radius: 20px;
    padding: 50px;
    animation-name: opacity;
    animation-duration: 1.5s;
    box-shadow: 0 2px 43px -4px rgba(0, 0, 0, 0.19) !important;
  }
  &__search {
    background: #e6e6e6;
    border-radius: 10px;
    border: 2px solid #ffffff;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 0.5em 0;
    padding: 0.5em 1em;
    transition: all 0.5s;
    -webkit-transition: all 0.5s;
    width: 450px;
    &:hover{
      border: 2px solid #d8d8d8;
    }
    &:focus{
      border: 2px solid #d8d8d8;
    }
    button{
      border: 0;
      outline: 0;
      padding: 0.3em 0.8em;
      border-radius: 10px;
      color: #fff;
      font-size: 1.3rem;
    }
    input {
      background: transparent;
      font-weight: 500;  
      border: 0;
      font-size: 1.4rem;
      outline: 0;
      width:75%;
      &::placeholder {
        color: #c2c2c2
      }
    }
  }
}

.card {
  transition: all 0.2s ease-out !important;
  box-shadow: 0 2px 20px -4px rgba(0, 0, 0, 0.19) !important;
  margin-bottom: 1.2rem;
  border-radius: 10px !important;
  border: none !important;
  animation-name: opacity;
  animation-duration: 1s;
  &:hover {
    transform: translateY(2px);
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.05) !important;
  }
  &-body{
    justify-content: space-between;
    display: flex;
    padding: 1rem 1.5rem!important;
    border-radius: 15px;
  }
  &__delate{
    animation-name: opacity;
    animation-duration: 1.2s;
    border-radius:10px !important;
    padding:10px !important;
    img{
      margin: 0px 10px;
      width: 15px;
      top: -2px;
      position: relative;
    }
    &-list{
      width: 15px;
    }
  }
  &__left {
    display: flex;
    width: 100%;
    input{
      margin: 12px 0;
    }
  }
  &__line{
    margin-left: 20px;
    font-size: 1.5rem;
    width: 320px;
    text-align: left;
  }
  &__taskdone{
    opacity: .5;
    transform: translateY(2px);
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.05);
    .card__line {
      text-decoration: line-through;
    }
  }
}

@media (max-width: 767px) {
  .todolist{
    &__main{
      width: 90%;
      padding: 50px 15px;
    }
    &__search{
      width: 100%;
      flex-direction: column;
      button{
        margin-top: 15px;
        width: 100%;
      }
      input {
        width: 100%;
      }
    }
  }
  .card{
    &__left{
      width: 83%;
    }
    &__line{
      width: 83%;
    }
  }
}
</style>