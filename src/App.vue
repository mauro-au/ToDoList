<template>
  <div id="main">
    <h2>{{ message }}</h2>
    <br />
    <label>Tarea</label>
    <input type="text" placeholder="Ingrese nueva tarea" v-model="tarea" />
    <button @click="guardarTarea">Crear</button>
    <br />

    <h3>Lista</h3>
    <ul class="container">
        <li v-for="(tarea, index) in tareas" :key="index">
            <input type="checkbox">{{index}}:{{tarea.name}}
        </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      message: "Crear una nueva tarea",
      tarea: "",
      tareas: [],
      mostrar: false
    };
  },
  methods: {
    mostrarNombre: function() {
      this.mostrar = !this.mostrar;
    },
    guardarTarea: function() {
        if(this.tarea !== ""){

            this.tareas.push({
              name: this.tarea
            });
        }
      this.tarea = "";
    }
  }
};
</script>
<style scoped>
#main {
  font-size: 25px;
  font-family: "Calibri", sans-serif;
  color: darkblue;
  text-align: center;
}
input{
    padding: 10px;
    margin: 0 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
}
button{
    padding: 10px 30px;
    background: #0e62ff;
    border-radius: 5px;
    border: none;
    color: #fff;
}
.container{
    width: 30%;
    margin: 30px auto 0 auto;
    text-align: left;
    padding-left: 132px;
}
</style>