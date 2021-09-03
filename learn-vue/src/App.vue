<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      title="Task tracker"
      :showAddTask="showAddTask"
    />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"      
      @toggle-update-task-text="updTaskText"       
      @deleteTask="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>



<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
      showUpdateTask: true,
    };
  },
  computed:{

  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    toggleUpdateTask() {
      this.showUpdateTask = !this.showUpdateTask;
    },
    updTaskText(id) {
      console.log("Update task, id: ", id);
    },
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task.");
      }
    },
    async toggleReminder(id) {
      // to update a part of db entry:
      //1. fetch the item
      const taskToToggle = await this.fetchTask(id);
      //define what to update
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      //make request to db server
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });

      // parse the data
      const data = await res.json();

      //in this instance we are accessing this.task (this, since we are accessing a specific data)
      this.tasks = this.tasks.map((task) =>
        //if the task id is equal to the id that is being passed,
        //the reminder is being set to the oppsite of the previous value, i.e. from true to false and vice versa
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
      // this.tasks = this.tasks.map((task) =>
      //       task.id === id ? { ...task, reminder: data.reminder } : task
      //     )
    },

    //the api is from the vue.config.js.
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>


<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
