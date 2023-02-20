<template>
  <div class="container bg" style="max-width: 600px">
    <!-- Heading -->
    <h2 class="text-center mt-5">Todo App</h2>
    
    <!-- Input -->
    <div class="d-flex mt-5">
      <input type="text" v-model="task" placeholder="Enter task"  class="w-100 form-control bg">
      <button class="btn btn-danger rounded-0" @click="submitTask">
        SUBMIT
      </button>
    </div>
    <!-- Task table -->
    <table class="table table-bordered mt-4 ">
      <thead>
        <tr>
          <th scope="col" class="text-center">Task</th>
          <th scope="col" class="text-center">Canc</th>
          <th scope="col" class="text-center">Edit</th>
        </tr>
      </thead>
      <tbody>
        <!-- Cycle up -->
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      editedTask: null,
      newTodo:'',
      tasks: [
      {
        name: "1kg di banane 2kg di patate 1kg di salmone",
        
      },
      {
        name: "cioccolato cocacola broccoli riso pollo.",
        
      },
      {
        name: "mele pere arancie pasta sugo avena.",
        
      },
      ],
    };
  },
  methods: {
    /**
    * Capitalize first character
    */
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
    /**
    * Change status of task by index
    */
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
    /**
    * Deletes task by index
    */
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    /**
    * Edit task
    */
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    /**
    * Add / Update task
    */
    submitTask() {
      if (this.task.length === 0) return;
      /* We need to update the task */
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        
        this.tasks.push({
          name: this.task,
        });
      }
      this.task = "";
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.line-through {
  text-decoration: line-through;
} 
.bg{
  background-color: rgb(203, 96, 88);
}
</style>