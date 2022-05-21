<template>
  <form @submit="onSubmit">
    <div>
      <label>Task</label>
      <input type="text" v-model="text" />
    </div>
    <div>
      <label>Day</label>
      <input type="text" v-model="day" />
    </div>
    <div>
      <label>Reminder</label>
      <input type="checkbox" v-model="reminder" />
    </div>
    <input type="submit" value="Save" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert("Please add a task");
        return;
      }
      const newTask = {
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      };

      this.$emit("add-task", newTask);

      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>
