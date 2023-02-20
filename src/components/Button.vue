<template>
  <button
    class="btn"
    :style="{
      backgroundColor: color,
    }"
    @click="onClick()"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: ["text", "color", "onclick"],
  methods: {
    onClick() {
      this.$emit("btn-clicked");
    },
  },
  emits: ["btn-clicked"],
};
</script>

<style scoped></style>
