<script setup>
    const props = defineProps (['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui itens a comprar" class="form-control">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas"> 🍍 Todos os itens</option>
                    <option value="pendentes"> 🥫  Falta buscar 🧀</option>
                    <option value="finalizadas"> 🍑  No carrinho 🥖</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style>
    select{
        text-align: center;
    }
</style>