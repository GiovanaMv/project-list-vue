<script setup>
    defineProps(['tarefasPendentes']);
</script>

<template>
    <header class="p-3 pt-4 mb-4 mt-4  rounded-3">
        <h1>Minha Lista de SuperMercado 🛒</h1>
        <p>
            Você possui {{ tarefasPendentes }} itens a buscar🍊🍉🍇
        </p>
    </header>
</template>

<style>
    header{
        background-color: rgb(255, 252, 93);
        text-align: center;
    }
    
</style>