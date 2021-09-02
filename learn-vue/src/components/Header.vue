<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @btn-click="$emit('toggle-add-task')"
      :color="showAddTask ? 'black' : 'green'"
      :btnText="showAddTask ? 'Close' : 'Add task'"
    />
    <!-- <Button color="blue" btnText="Update task"/>
    <Button color="red" btnText="Delete task"/> -->
  </header>
</template>

<script>
import Button from "./Button";

export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "Well hello there.", //this is strictly not needed, but is to show that multiple ways are possible
    }, showAddTask: Boolean,
  },
  components: {
    Button,
  },
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