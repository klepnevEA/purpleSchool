<script setup>
    import { inject } from "vue";
    import Card from "./Card.vue";
    const cardsList = inject("cardsList");
    console.log(cardsList);
</script>

<template>
 <main class="main">
 <template v-for="(item, index) in cardsList" :key="index">
     <Card  :cardInfo="item" :id="index" />
 </template>
</main>
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
