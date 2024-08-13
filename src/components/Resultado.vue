
<!-- passando a propriedade que esse componente vai usar que vai ser o resultado do calculo -->
<script setup>
const props = defineProps(['resultado']);
</script>

<template>
    <div>Resultado: {{ resultado }}</div>
</template>
  
  
  