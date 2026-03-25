<script setup>
  
    import Card from "./Card.vue";
</script>

<template>
 <main class="main"><Card /></main>
</template>

<style scoped>
.main {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: auto;
    gap: 49px;
    padding: 37px;
    justify-items: center;
}
</style>
