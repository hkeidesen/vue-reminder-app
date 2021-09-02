<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" v-bind:class="[task.reminder ? 'reminder' : '', 'task']">
      <!-- we need to add ", task" since we always want to display the task! -->
    <h3>
      {{ task.text }}
      <!-- fas = font awesome class -->
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
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
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>