<template>
  <button @click="onClick()">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: ["text"],
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>
