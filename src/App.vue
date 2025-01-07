<script setup>
import { reactive } from 'vue';
import Header from './components/Cabecalho.vue'
import Form from './components/Formulario.vue'
import ToDo from './components/ListaTarefa.vue'

  const state = reactive({
    filter: 'all',

    taskTemp: '',

    tasks: []
  })

  const getPendingTasks = () => {
    return state.tasks.filter(task => !task.completed)
  }

  const getCompletedTasks = () => {
    return state.tasks.filter(task => task.completed)
  }

  const getFilteredTasks = () => {
    const { filter } = state

    switch(filter) {
      case 'pending':
        return getPendingTasks()

      case 'completed':
        return getCompletedTasks()

      default: 
        return state.tasks
    }
  }

  const changeFilterTemp = (event) => {
    state.filter = event.target.value
  }

  const addTask = () => {
    const newTask = {
      title: state.taskTemp,
      completed: false
    }

    state.tasks.push(newTask)
    state.taskTemp = '' // clears the input field after adding the task
  }

  const editTaskTemp = (event) => {
    state.taskTemp = event.target.value
  }
</script>

<template>
  <div class="container">
    <Header :pending-tasks="getPendingTasks().length"/>
    <Form :change-filter="changeFilterTemp" :task-temp="state.taskTemp" :edit-task-temp="editTaskTemp" :add-task="addTask"/>
    <ToDo :tasks="getFilteredTasks()"/>
  </div>
</template>