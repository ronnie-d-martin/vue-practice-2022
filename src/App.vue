<template>
  <div class="container">
    <HeaderComponent
    :showAddTask="showAddTask"
    @toggle-add-task="toggleAddTask" 
    title="Task Tracker" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>

    <TasksComponent
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import HeaderComponent from "./components/Header";
import TasksComponent from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
  name: "App",
  components: {
    HeaderComponent,
    TasksComponent,
    AddTask,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Maglaba",
          day: "December 1 2022",
          reminder: true,
        },
        {
          id: 2,
          title: "Magsaing",
          day: "December 10 2022",
          reminder: true,
        },
        {
          id: 3,
          title: "Maglagay ng Tubig",
          day: "December 20 2022",
          reminder: false,
        },
      ],
      showAddTask: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },

    addTask(task) {
      this.tasks = [...this.tasks, task];
    },

    deleteTask(id) {
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },

  // created(){
  //   this.tasks = [
  //   {
  //       id: 1,
  //       title: 'Maglaba',
  //       day: 'December 1 2022',
  //       reminder: true,
  //     },
  //     {
  //       id: 2,
  //       title: 'Magsaing',
  //       day: 'December 10 2022',
  //       reminder: false,
  //     },
  //     {
  //       id: 3,
  //       title: 'Maglagay ng Tubig',
  //       day: 'December 20 2022',
  //       reminder: false,
  //     },
  //   ]
  // }
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
