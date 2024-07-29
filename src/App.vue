<script setup>
import { reactive } from 'vue';
import Header from './components/Cabecalho.vue'
import Form from './components/Formulario.vue'
import To_do from './components/ListaTarefa.vue'

  const estado = reactive({
    filtro: 'todas',

    tarefaTemp: '',

    tarefas: []
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltardas = () => {
    const { filtro } = estado

    switch(filtro) {
      case 'pendentes':
        return getTarefasPendentes()

      case 'finalizadas':
      return getTarefasFinalizadas()

      default: 
        return estado.tarefas
    }
  }

  const trocaFiltroTemp = (evento) => {
    estado.filtro = evento.target.value
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }

    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '' // limpa o campo de input após o cadastro
  }

  const editaTarefaTemp = (evento) => {
    estado.tarefaTemp = evento.target.value
  }
</script>

<template>
  <div class="container">
    <Header :tarefas-pendentes="getTarefasPendentes().length"/>
    <Form :trocar-filtro="trocaFiltroTemp" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="editaTarefaTemp" :cadastra-tarefa="cadastraTarefa"/>
    <To_do :tarefas="getTarefasFiltardas()"/>
  </div>
</template>