<script setup>
import {reactive} from 'vue'
import Cabecalho from './components/Cabecalho.vue'
import Formaulario from './components/Formulario.vue'
import ListaTarefas from './components/ListaTarefas.vue'



const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas:[
    {
    titulo: 'Estudar ES6',
    finalizada: false,
  },{
    titulo: 'Estudar SASS',
    finalizada: false,
  },{
    titulo: 'Ir para a academia',
    finalizada: true,
  }
    ]})

  const getTarefasPendentes = () =>{
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFInalizadas = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () =>{
    const {filtro} = estado

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes()
    
      case 'finalizadas':
        return getTarefasFInalizadas()

      default:
        return estado.tarefas 
    }
  }

  const cadastraTarefa = ()=>{
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ''
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formaulario :trocar-filtro="e=>estado.filtro = e.target.value" :terefa-temp="estado.tarefaTemp" :edita-tarefa-temp="e => estado.tarefaTemp = e.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaTarefas :tarefas="getTarefasFiltradas()"/> 
       
 
  </div>
</template>

