<script setup>
    import { inject } from "vue";
    import Count from "./ui/Count.vue";
    const countStore = inject("count");
</script>

<template>
 <header class="head">
    <div class="head__title">ЗАПОМНИ СЛОВО</div>
    <Count :count="countStore" />
 </header>
</template>

<style scoped>
.head {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 27px 62px;
}

.head__title {
    text-transform: uppercase;
    color: var(--secondary-color);
    font-weight: 700;
}
</style>
