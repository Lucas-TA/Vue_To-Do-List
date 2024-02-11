<script setup lang="ts">
    const props = defineProps(['assignTask', 'inputTask', 'newTask', 'filter'])
</script>
<template>
    <form @submit.prevent="props.assignTask">
        <div class="row">
            <div class="col">
                <input :value="props.inputTask"
                    @change="props.newTask" required
                    type="text" placeholder="Descrição da Tarefa" class="form-control" />
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.filter"
                    class="form-control">
                    <option value="all">Todas as Tarefas</option>
                    <option value="pending">Pendentes</option>
                    <option value="finished">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>