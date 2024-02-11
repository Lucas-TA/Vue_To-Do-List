<script setup lang="ts">
    const props = defineProps(['PendingTasks'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p>
            Você Possui {{ props.PendingTasks }} tarefas pendentes
        </p>
    </header>
</template>