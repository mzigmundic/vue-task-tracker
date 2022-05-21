<template>
  <div :class="[task.reminder ? `reminder` : ``, `task`]">
    <div>
      <h3>{{ task.text }}</h3>
      <p>{{ task.day }}</p>
    </div>
    <div>
      <button @click="$emit(`toggle-task`, task.id)">Toggle</button>
      <button @click="$emit(`delete-task`, task.id)">Remove</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>

<style scoped>
.task {
  display: flex;
  justify-content: space-between;
  background-color: grey;
  border-bottom: 2px solid black;
}
.reminder {
  background-color: chartreuse;
}
</style>
