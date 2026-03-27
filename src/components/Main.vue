<script setup>
    import { inject } from "vue";
    import Button from "./ui/Button.vue";
    import Card from "./Card.vue";
    const cardsList = inject("cardsList");


    const emit = defineEmits(['newGame'])
    
    const newGame = () => {
        emit('newGame')
    }
</script>

<template>
 <main class="main">
 <template v-for="(item, index) in cardsList" :key="index">
     <Card  :cardInfo="item" :id="index" />
 </template>

</main>
<div class="footer">
     <Button @click="newGame()">Начать зано</Button>
</div>
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

.footer {
    display: flex;
    justify-content: center;
    padding: 37px;
}
</style>
