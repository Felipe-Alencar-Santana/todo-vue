<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa.id">
            <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.id" type="checkbox">
            <label :class="{ 'done': tarefa.concluida }" class="ms-3" :for="tarefa.id">
                {{ tarefa.descricao }} <!--Aqui estamos usando a diretiva v-for para iterar sobre o array de tarefas e exibir cada tarefa na tela. E como o array de tarefas tem os valores [{ id: 1, descricao: 'Estudar Vue.js', concluida: false }, { id: 2, descricao: 'Fazer exercícios de Vue.js', concluida: false }, { id: 3, descricao: 'Criar um projeto com Vue.js', concluida: false }], ele vai exibir "Estudar Vue.js", "Fazer exercícios de Vue.js" e "Criar um projeto com Vue.js" na tela.-->
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>
