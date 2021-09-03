<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    v-bind:class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <!-- we need to add ", task" since we always want to display the task! -->
    <h3>
      {{ task.text }}

      <!-- fas = font awesome class -->
      <i @click="$emit('toggle-update-task-text', task.id)" class="fas fa-edit">
      
      </i>
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </h3>

    <p>{{ task.day }}</p>

    <!-- 
      
      
      <h3 v-if="false">
      <input v-if="false" :placeholder="[[task.text]]" />
      <i
        @click="$emit('toggle-save-task-text', task.id)"
        class="fas fa-save"
      ></i>
    </h3> -->
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
i.fas.fa-times::before {
  color: red;
}
i.fas.fa-edit::before {
  color: rgb(0, 0, 0);
}
input {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.update {
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
.task i {
  justify-content: right;
}
</style>