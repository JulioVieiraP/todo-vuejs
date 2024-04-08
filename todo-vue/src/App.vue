<script setup>
import { reactive } from 'vue'
import Cabeçalho from './components/Cabeçalho'
import Formulario from "./components/Formulario";
import Lista from "./components/lista";

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false
    },
    {
      titulo: 'Ie para a academia',
      finalizada: true,
    },
  ]
})

const getTarefasPendentes = () =>{
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () =>{
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () =>{
  const {filtro} = estado

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes()
      
    case 'finalizadas':
      return getTarefasFinalizadas()
      
    default:
      return estado.tarefas
      
  }
}

const cadastraTarefa = () =>{
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }

  estado.tarefas.push(tarefaNova)
  estado.tarefaTemp =''  
}

</script>

<template>
  <div class="container">
    <Cabeçalho tarefa />
    <Formulario/>
    <Lista/>
    
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
