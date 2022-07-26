<template>
  <div class="container">
    <h2 class="text-center mt-5">MY Vue Todo App</h2>
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" />
      <button @click="addtodo()" type="button" class="btn btn-warning">
        SUBMIT
      </button>
    </div>
    <div class="list-todos mt-5">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col" class="text-center">#</th>
            <th scope="col" class="text-center">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in tasks" :key="index">
            <td>{{ todo.name }}</td>
            <td style="width: 120px">
              <span @click="changeStatus(index)" class="pointer">{{
                firstCharUpper(todo.status)
              }}</span>
            </td>
            <td>
              <div @click="edittask(index)" class="text-center">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td>
              <div @click="deletetodo(index)" class="text-center">
                <span class="fa fa-trash"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      tasks: [
        {
          name: "Temizlik işini yap",
          status: "to-do",
        },
      ],
      task: " ",
      editTask: null,
      avaliable: ["to-do", "in-progress", "finished"],
    };
  },
  methods: {
    addtodo() {
      if (this.task.length === 0) return;

      if (this.editTask === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.editTask].name = this.task;
        this.editTask = null;
      }
      this.task = " ";
    },
    deletetodo(index) {
      this.tasks.splice(index, 1);
    },
    edittask(index) {
      this.task = this.tasks[index].name;
      this.editTask = index;
    },
    changeStatus(index) {
      let newIndex = this.avaliable.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.avaliable[newIndex];
    },
    firstCharUpper(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },
};
</script>
<style scoped>
.container {
  margin: auto;
  width: 40%;
}
.pointer {
  cursor: pointer;
}
</style>
