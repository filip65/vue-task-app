<template>
  <Task
    v-for="task in tasks"
    :key="task.id"
    :task="task"
    @task-delete="$emit('task-delete', task.id)"
    @task-toggle="$emit('task-toggle', task.id)"
  />
</template>

<script>
import Task from "@/components/Task.vue";

export default {
  name: "Tasks",
  components: { Task },
  props: {
    tasks: {
      type: Array,
    },
  },
  methods: {
    logger(text) {
      console.log("je to:", text);
    },
  },
  emits: ["task-delete", "task-toggle"],
};
</script>

<style scoped></style>
