<script setup>
  
</script>

<template>
 <button class="button"><slot /></button>
</template>

<style scoped>
.button {
    background-color: var( --button-bg-color);
    color: var(--primary-color);
    padding: 16px 10px;
    min-width: 335px;
    border-radius: 100px;
    border: none;
    text-align: center;
    cursor: pointer;
    font-size: 24px;
}
</style>
