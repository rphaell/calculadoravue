
<!-- passando as propriedades e funcoes que sao usadas no componente -->
<script setup>
const props = defineProps(['numero1', 'numero2', 'operacao', 'atualizaNumero1', 'atualizaNumero2', 'atualizaOperacao']);
</script>


<template>
    <div>
        <h1 style="text-align: center; font-size: 70px; margin-bottom: 20px;">Calculadora</h1>
        <input type="number" :value="numero1" @input="atualizaNumero1" placeholder="Número 1" />
        <input type="number" :value="numero2" @input="atualizaNumero2" placeholder="Número 2" />
        <select @change="atualizaOperacao" :value="operacao">
            <option value="soma">Soma</option>
            <option value="subtracao">Subtração</option>
        </select>
    </div>
</template>