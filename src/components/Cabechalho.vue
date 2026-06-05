<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <div class="p-5 mb-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            Voce possui {{ props.tarefasPendentes }} tarefas pendentes.
        </p>
    </div>
</template>