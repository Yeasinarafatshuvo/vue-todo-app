<template>
  <div class="container">
    <h2>My Vue Todo App</h2>

    <!-- input -->
    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter Task"
        class="form-control"
      />
      <button @click="submitTask" class="btn btn-warning rounded-0">
        SUBMIT
      </button>
    </div>

    <!-- Task Table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td>
            <span @click="changeStatus(index)">{{
              firstCharUpper(task.status)
            }}</span>
          </td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen" style="cursor: pointer"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash" style="cursor: pointer"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      editedTask: null,
      availableProgress: ["todo", "In-Progress", "finished"],
      tasks: [
        {
          name: "Lorem ipsum dolor sit, amet consectetur adipisicing elit.",
          status: "to-do",
        },
        {
          name: "Lorem ipsum dolor sit, amet consectetur adipisicing elit.",
          status: "to-do",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.task === 0) return;
      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = "";
    },
    deleteTask(key) {
      this.tasks.splice(key, 1);
    },
    editTask(key) {
      this.task = this.tasks[key].name;
      this.editedTask = key;
    },

    changeStatus(key) {
      let newIndex = this.availableProgress.indexOf(this.tasks[key].status);
      newIndex++;
      if (newIndex > 2) newIndex = 0;
      this.tasks[key].status = this.availableProgress[newIndex];
    },

    firstCharUpper(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },
};
</script>

<style></style>
