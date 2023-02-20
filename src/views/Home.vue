<template>
  <AddTask @add-task="addTask" v-if="showForm" />
  <Tasks :tasks="tasks" @task-delete="deleteTask" @task-toggle="toggleTask" />
</template>

<script>
import AddTask from "@/components/AddTask.vue";
import Tasks from "@/components/Tasks.vue";
export default {
  name: "Home",
  props: {
    showForm: Boolean,
  },
  components: { Tasks, AddTask },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });

      if (res.status === 200) {
        this.tasks = this.tasks.filter((item) => item.id !== id);
      } else {
        alert("Failed to delete task :(");
      }
    },
    async toggleTask(id) {
      const taskToToggle = await this.fetchTask(id);

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify({
          ...taskToToggle,
          reminder: !taskToToggle.reminder,
        }),
      });

      if (res.status === 200) {
        this.tasks = this.tasks.map((task) =>
          task.id === id ? { ...task, reminder: !task.reminder } : task
        );
      }
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
      this.$emit("toggle-add-form");
      // this.showForm = false;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const res = await fetch("api/tasks");
    const data = await res.json();

    this.tasks = data;
  },
  emits: ["toggle-add-form"],
};
</script>

<style scoped></style>
