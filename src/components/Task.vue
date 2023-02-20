<template>
  <div
    :class="[task.reminder ? 'reminder' : '', 'task']"
    @dblclick="$emit('task-toggle')"
  >
    <h3>
      {{ task.text }} <i class="fas fa-times" @click="$emit('task-delete')"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: {
      text: String,
      day: String,
      reminder: Boolean,
    },
  },
  emits: ["task-delete", "task-toggle"],
};
</script>

<style scoped>
.task {
  background-color: #f4f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
  border-left: 5px solid transparent;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.fas {
  color: red;
}
</style>
