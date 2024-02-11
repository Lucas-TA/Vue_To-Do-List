<script setup lang="ts">
import { reactive } from 'vue'
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import TaskList from './components/TaskList.vue'

interface Task {
  title: string;
  isFinished: boolean;
}

interface State {
  filter: string;
  inputTask: string;
  newTask: Task;
  tasks: Task[];
}

const state:State = reactive<State>({
  filter: 'all',
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
});

const getPendingTasks = (): Task[] => {
  return state.tasks.filter(task => !task.isFinished);
};

const getFinishedTasks = (): Task[] => {
  return state.tasks.filter(task => task.isFinished);
};

const getFilteredTasks = (): Task[] => {
  const { filter } = state;

  switch(filter) {
    case 'pending':
      return getPendingTasks();
    case 'finished':
      return getFinishedTasks();
    default:
      return state.tasks;
  }
};

const assignTask = () => {
  if (state.newTask.title.trim() !== '') {
    const newTaskObj: Task = {
      title: state.newTask.title,
      isFinished: false,
    };
    state.tasks.push(newTaskObj);
    state.newTask.title = '';
  }
};
</script>

<template>
  <div class="container">
    <Header :PendingTasks="getPendingTasks().length"/>
    <Form 
      :inputTask="state.inputTask" 
      :newTask="(e:any) => { if (e.target) state.newTask.title = (e.target as HTMLInputElement).value }"
      :assignTask="assignTask"
      :filter="(e:any)=> { if (e.target) state.filter = (e.target as HTMLOptionElement).value }"
    />
    <TaskList :getFilteredTasks="getFilteredTasks()"/>
  </div>
</template>
