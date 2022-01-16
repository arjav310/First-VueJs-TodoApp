<template>
  <div class="container">
    <h1>TODO App</h1>

    <!-- Input -->
    <div class="d-flex">
      <input
        v-model="newTask"
        type="text"
        placeholder="Enter a task"
        class="form-control"
      />
      <button v-on:click="addItem" class="btn btn-warning" type="submit">
        ADD
      </button>
    </div>

    <!-- Task Table -->

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ finished: task.status === 'Finished' }">{{
              task.name
            }}</span>
          </td>
          <td style="width: 120px">
            <span
              v-on:click="changeStatus(index)"
              class="pointer"
              :class="{
                'text-danger': task.status === 'To-do',
                'text-warning': task.status === 'In-progress',
                'text-success': task.status === 'Finished',
              }"
              >{{ task.status }}</span
            >
          </td>
          <td>
            <div id="edit" class="text-center" v-on:click="editTask(index)">
              <span class="fa fa-pen pointer"> </span>
            </div>
          </td>
          <td>
            <div id="delete" class="text-center" v-on:click="deleteTask(index)">
              <span class="fa fa-trash pointer"> </span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: {
    title: String,
  },

  data() {
    return {
      tasks: [
        {
          name: "Steal bananas from the store.",
          status: "To-do",
        },
        {
          name: "Eat Chocolate",
          status: "In-progress",
        },
      ],
      newTask: "",
      editedTask: null,
      availableStatus: ["To-do", "In-progress", "Finished"],
    };
  },
  methods: {
    addItem: function () {
      if (this.tasks.length === 0) return;

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.newTask,
          status: "To-do",
        });
      } else {
        this.tasks[this.editedTask].name = this.newTask;
        this.editedTask = null;
      }

      this.newTask = "";
    },

    deleteTask: function (index) {
      this.tasks.splice(index, 1);
    },

    editTask: function (index) {
      this.newTask = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus: function (index) {
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status);

      if (++newIndex > 2) newIndex = 0;

      this.tasks[index].status = this.availableStatus[newIndex];
    },
  },
};
</script>

<style>
#delete:hover {
  color: red;
}
#edit:hover {
  color: green;
}
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
}
</style>
