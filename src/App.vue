<script setup>
import { reactive} from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';
import Formulario from './components/Formulario.vue';

const estado = reactive ({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas:[
    {
      titulo: 'arroz',
      finalizada: false,
    },
    {
      titulo: 'abacaxi',
      finalizada: false,
    },
    {
      titulo: 'carne',
      finalizada: true,
    },
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}
const cadastratarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastratarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


