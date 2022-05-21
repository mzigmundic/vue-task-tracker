<template>
  <AddTask  v-if="showAddTask" @add-task="addTask" />
  <Tasks @delete-task="deleteTask" @toggle-task="toggleTask" :tasks="tasks" />
</template>

<script>
import Tasks from "../components/Tasks";
import AddTask from "../components/AddTask";

export default {
  name: "Home",
  props: {
    showAddTask: Boolean
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async addTask(task) {
      const res = await fetch("/api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async toggleTask(id) {
      const taskToToggle = await this.fetchTask(id);
      const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updatedTask),
      });
      const data = await res.json();
      this.tasks = this.tasks.map((task) => {
        if (task.id === id) {
          return { ...task, reminder: data.reminder };
        } else {
          return task;
        }
      });
    },
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });
      if (res.status === 200) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      } else {
        alert("Error deleting task");
      }
    },
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
