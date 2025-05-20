<script setup>
const props = defineProps(['tasks'])
</script>

<template>
  <ul v-if="props.tasks.length > 0" class="list-group mt-4">
    <li class="list-group-item" v-for="task in props.tasks">
      <input
        @change="(event) => (task.done = event.target.checked)"
        :checked="task.done"
        :id="task.title"
        type="checkbox"
      />
      <label :class="{ done: task.done }" class="ms-3" :for="task.title">{{ task.title }}</label>
    </li>
  </ul>
  <p v-else class="mt-4">Nenhuma tarefa Pendente</p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
