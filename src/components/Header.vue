<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-show="homepage"
      :text="showAddForm ? 'Close' : 'Add Task'"
      :color="showAddForm ? 'red' : 'green'"
      @btn-clicked="$emit('toggle-add-form')"
    />
  </header>
</template>

<script>
import Button from "@/components/Button.vue";

export default {
  name: "Header",
  props: {
    title: String,
    showAddForm: Boolean,
  },
  computed: {
    homepage() {
      return this.$route.path === "/";
    },
  },
  components: {
    Button,
  },
  emits: ["add-task-toggle", "toggle-add-form"],
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
