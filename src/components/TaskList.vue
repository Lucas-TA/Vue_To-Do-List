<script setup lang="ts">
    const props = defineProps(['getFilteredTasks'])
</script>
<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="task in props.getFilteredTasks">
        <input
            @change="e => {if (e.target) task.isFinished = (e.target as HTMLInputElement).checked}"
            :checked="task.isFinished"
            :id="task.title"
            type="checkbox"
        />
        <label :class="{ done: task.isFinished }" :for="task.title" class="ms-3">
            {{ task.title }}
        </label>
        </li>
    </ul>
</template>
<style scoped>
    .done {
    text-decoration: line-through;
    }
</style>
