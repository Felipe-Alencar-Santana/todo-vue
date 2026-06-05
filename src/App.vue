<script setup>
import { reactive } from 'vue';
import Cabechalho from './components/Cabechalho.vue';
import Formulario from './components/Formulario.vue';
import Lista from './components/Lista.vue';

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
    <Cabechalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :tarefa-temp="estados.tarefaTemp" :editar-tarefa-temp="evento => estados.tarefaTemp = evento.target.value" :filtro="evento => estados.filtro = evento.target.value" :cadastrar="adicionarTarefa"/>
    <Lista :tarefas="getTarefasFiltradas()"/>
  </header>
</template>
