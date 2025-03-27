<script setup>
import { reactive, watch, onMounted } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';
import Formulario from './components/Formulario.vue';

const estado = reactive ({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: []
});

// Função para carregar as tarefas salvas no LocalStorage
onMounted(() => {
  const tarefasSalvas = localStorage.getItem('listaSupermercado');
  if (tarefasSalvas) {
    estado.tarefas = JSON.parse(tarefasSalvas);
  }
});

// Função para salvar no LocalStorage sempre que a lista mudar
watch(() => estado.tarefas, (novoValor) => {
  localStorage.setItem('listaSupermercado', JSON.stringify(novoValor));
}, { deep: true });

const getTarefasPendentes = () => estado.tarefas.filter(tarefa => !tarefa.finalizada);
const getTarefasFinalizadas = () => estado.tarefas.filter(tarefa => tarefa.finalizada);

const getTarefasFiltradas = () => {
  switch(estado.filtro){
    case 'pendentes': return getTarefasPendentes();
    case 'finalizadas': return getTarefasFinalizadas();
    default: return estado.tarefas;
  }
};

const cadastratarefa = () => {
  if (estado.tarefaTemp.trim() === '') return;

  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
};

// Função para limpar a lista quando clicar no botão "Limpar Lista"
const limparLista = () => {
  estado.tarefas = [];
  localStorage.removeItem('listaSupermercado');
};

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastratarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
    <button @click="limparLista" class="btn btn-danger mt-3">Limpar Lista</button>
  </div>
</template>
