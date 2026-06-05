<script setup>
    const props = defineProps(['cadastrar', 'tarefaTemp', 'filtro', 'editarTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastrar">
        <div class="row">
            <div class="col">
            <input :value="props.tarefaTemp" @change="props.editarTarefaTemp" required type="text" class="form-control" placeholder="Digite sua tarefa">
            </div>
            <div class="col-md-2">
            <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
            <select @change="props.filtro" class="form-control" id="">
                <option value="Todas">Todas as tarefas</option>
                <option value="Pendentes">Tarefas pendentes</option>
                <option value="Concluídas">Tarefas concluídas</option>
            </select>
            </div>
        </div>
    </form>
</template>