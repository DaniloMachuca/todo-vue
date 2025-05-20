<script setup>
import { reactive } from 'vue'

const state = reactive({
  filter: 'todas',
  tempTask: '',
  tasks: [
    {
      title: 'Estudar Vue',
      done: false,
    },
    {
      title: 'Estudar Sass',
      done: false,
    },
    {
      title: 'Ir para academia',
      done: true,
    },
  ],
})

const getTarefasPendentes = () => {
  return state.tasks.filter((task) => !task.done)
}

const getTarefasFinalizadas = () => {
  return state.tasks.filter((task) => task.done)
}

const getTarefasFiltradas = () => {
  const { filter, tasks } = state
  switch (filter) {
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return state.tasks
  }
}

const cadastraTarefa = () => {
  const newTask = {
    title: state.tempTask,
    done: false,
  }
  state.tasks.push(newTask)
  state.tempTask = ''
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você tem {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input
            :value="state.tempTask"
            @change="(event) => (state.tempTask = event.target.value)"
            required
            type="text"
            placeholder="Digite a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="(event) => (state.filter = event.target.value)" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="finalizadas">Tarefas Finalizadas</option>
            <option value="pendentes">Tarefas Pendentes</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getTarefasFiltradas()">
        <input
          @change="(event) => (task.done = event.target.checked)"
          :checked="task.done"
          :id="task.title"
          type="checkbox"
        />
        <label :class="{ done: task.done }" class="ms-3" :for="task.title">{{ task.title }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
