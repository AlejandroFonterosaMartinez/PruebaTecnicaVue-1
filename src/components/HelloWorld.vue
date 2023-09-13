<template>
  <h1>Lista de Tareas</h1>
  <div>
    <div class="container">
      <input id="tarea" class="form-control " v-model="newTask" @keyup.enter="addTask"
        placeholder="Agregar nueva tarea" />
      <button id="agregar" class="btn btn-primary" @click="addTask">Agregar</button>
    </div>
  </div>
  <table class="table responsive">
    <thead>
      <tr>
        <th>Tarea</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody v-for="(task, index) in tasks" :key="index">
      <tr v-bind:class="{ 'completada': task.completed }">

        <th >{{ task.title }}</th>

        <th>
          <button id="completar" class="btn btn-success" @click="completeTask(index)">Completar</button>
          <button class="btn btn-danger" @click="deleteTask(index)">Eliminar</button>
        </th>
      </tr>
    </tbody>

  </table>
</template>

<script>
export default {
  data() {
    return {
      tasks: [] || localStorage.getItem("tasks") ? JSON.parse(localStorage.getItem("tasks")) : [],
      newTask: "",
      completed: false
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ title: this.newTask, completed: false });
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
        this.newTask = "";
      }
    },
    completeTask(index) {
      this.tasks[index].completed = true;
      localStorage.setItem("completedTasks", JSON.stringify(this.tasks));


    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },


  }
};
</script>
<style>
body {
  display: flex;
  justify-content: center;
  align-items: center;

}

#agregar {
  margin-left: 15px;
}

.completada {
  text-decoration: line-through;
  color: blue;
  font-style: italic;
}

#completar {
  margin-right: 15px;
}

.container {
  margin-top: 20px;
  margin-bottom: 20px;
  margin-left: 20px;
  margin-right: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f2f2f2;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* Center vertically */
  justify-content: center;

  font-size: 20px;
  text-align: center;
  /* Center horizontally */
}

#tarea {

  margin-bottom: 15px;
}
</style>