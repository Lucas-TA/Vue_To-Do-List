<script setup lang="ts">
import { reactive } from 'vue';

  const state = reactive({
    filter: 'All',
    inputTask: '',
    newTask: {
      title: '',
      isFinished: false,
    },
    tasks: [
      {
        title: 'Estudar ES6',
        isFinished: false,
      },
      {
        title: 'Estudar SASS',
        isFinished: false,
      },
      {
        title: 'Ir para a academia',
        isFinished: true,
      },
    ]
  })
  const getPendingTasks = () => {
    return state.tasks.filter(task => !task.isFinished)
  }
  const getFinishedTasks = () => {
    return state.tasks.filter(task => task.isFinished)
  }
  const getFilteredTasks = () => {
    const { filter } = state;

    switch(filter) {
      case 'pending':
        return getPendingTasks();
      case 'finished':
        return getFinishedTasks();
      default:
        return state.tasks;
    }

  }
  const assignTask = () => {
    const newTaskObj = {
      title: state.newTask.title,
      isFinished: false,
    }
    state.tasks.push(newTaskObj);
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você Possui {{ getPendingTasks().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="assignTask">
      <div class="row">
        <div class="col">
          <input :value="state.inputTask" @change="e => {if(e.target) state.newTask.title = (e.target as HTMLInputElement).value}" required type="text" placeholder="Descrição da Tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="e => {if(e.target) state.filter = (e.target as HTMLOptionElement).value}" class="form-control">
            <option value="all">Todas as Tarefas</option>
            <option value="pending">Pendentes</option>
            <option value="finished">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilteredTasks()">
        <input @change="e => {if (e.target) task.isFinished = (e.target as HTMLInputElement).checked}" :checked="task.isFinished" :id="task.title" type="checkbox">
        <label :class="{done: task.isFinished}" :for="task.title" class="ms-3">
          {{ task.title }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
