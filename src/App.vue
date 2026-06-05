<script setup>
import { reactive } from 'vue';

  const estados = reactive({
    filtro: 'Todas',
    tarefaTemp: '',
    tarefa: [
      { id: 1, descricao: 'Estudar Vue.js', concluida: false },
      { id: 2, descricao: 'Fazer exercícios de Vue.js', concluida: true },
      { id: 3, descricao: 'Criar um projeto com Vue.js', concluida: false },
    ],
    novaTarefa: '',
    filtro: 'Todas',
  })

  const getTarefasPendentes = () => {
    return estados.tarefa.filter(tarefa => !tarefa.concluida);
  }

  const getTarefasConcluidas = () => {
    return estados.tarefa.filter(tarefa => tarefa.concluida);
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estados;
    switch (filtro) {
      case 'Pendentes':
        return getTarefasPendentes();
      case 'Concluídas':
        return getTarefasConcluidas();
      default:
        return estados.tarefa;
    }
  }

  const adicionarTarefa = () => {
    const novaTarefa = {
      id: Date.now(),
      descricao: estados.tarefaTemp,
      concluida: false,
    }
    estados.tarefa.push(novaTarefa);
    estados.tarefaTemp = '';
  }
</script>

<template>
  <header class="container">
    <div class="p-5 mb-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Voce possui {{ getTarefasPendentes().length }} tarefas pendentes.
      </p>
    </div>
    <form @submit.prevent="adicionarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estados.tarefaTemp" @change="evento => estados.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Digite sua tarefa">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estados.filtro = evento.target.value" class="form-control" id="">
            <option value="Todas">Todas as tarefas</option>
            <option value="Pendentes">Tarefas pendentes</option>
            <option value="Concluídas">Tarefas concluídas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()" :key="tarefa.id">
        <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.id" type="checkbox">
        <label :class="{ 'done': tarefa.concluida }" class="ms-3" :for="tarefa.id">
            {{ tarefa.descricao }} <!--Aqui estamos usando a diretiva v-for para iterar sobre o array de tarefas e exibir cada tarefa na tela. E como o array de tarefas tem os valores [{ id: 1, descricao: 'Estudar Vue.js', concluida: false }, { id: 2, descricao: 'Fazer exercícios de Vue.js', concluida: false }, { id: 3, descricao: 'Criar um projeto com Vue.js', concluida: false }], ele vai exibir "Estudar Vue.js", "Fazer exercícios de Vue.js" e "Criar um projeto com Vue.js" na tela.-->
        </label>
      </li>
    </ul>
  </header>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
