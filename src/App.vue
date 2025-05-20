<script setup>
import { reactive } from 'vue'
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario
      :trocar-filtro="(event) => (state.filter = event.target.value)"
      :temp-task="state.tempTask"
      :edit-temp-task="(event) => (state.tempTask = event.target.value)"
      :cadastra-tarefa="cadastraTarefa"
    />
    <ListaDeTarefas :tasks="getTarefasFiltradas()" />
  </div>
</template>
