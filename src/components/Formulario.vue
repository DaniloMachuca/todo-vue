<script setup>
const props = defineProps(['cadastraTarefa', 'tempTask', 'trocarFiltro', 'editTempTask'])
</script>

<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col">
        <input
          :value="props.tempTask"
          @change="props.editTempTask"
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
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas as Tarefas</option>
          <option value="finalizadas">Tarefas Finalizadas</option>
          <option value="pendentes">Tarefas Pendentes</option>
        </select>
      </div>
    </div>
  </form>
</template>
