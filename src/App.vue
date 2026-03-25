<script setup>
  import Button from "./components/ui/Button.vue";
  import Main from "./components/Main.vue";
  import Head from "./components/Head.vue";
  import {ref, provide} from "vue";

  const isGameStart = ref(false);
  const statrGame = () => {
    isGameStart.value = !isGameStart.value
  }

  const count = ref(10);
  const cardsList = ref([
    {
      word: "man",
      translation: "мужик",
      state: "closed",
      status: "pending"
    },
    {
      word: "woman",
      translation: "женщина",
      state: "closed",
      status: "pending"
    }
  ])

const handleCardEvent = (cardIndex, cardAction) => {
  if (cardIndex < 0 || cardIndex >= cardsList.value.length) return;

  const card = cardsList.value[cardIndex];
  if (cardAction === 'turnOf') card.state = 'opened';
  else if (cardAction === 'noGuess' && card.status === 'pending') card.status = 'fail';
  else if (cardAction === 'guess' && card.status === 'pending') card.status = 'success';
};

  provide("count", count);
  provide('cardsList', cardsList);
  provide('cardEvent', handleCardEvent)


</script>

<template>
<div class="wrapper">
  <Head class="wrapper__head" />
  <div class="wrapper__content" v-if="!isGameStart">
    <Button @click="statrGame()">Начать игру</Button>
  </div>
  <Main class="wrapper__game" v-else />
</div>
 
 
</template>

<style scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    height: 100%;
    max-width: 1440px;
    margin: 0 auto;
  }

  .wrapper__content {
    flex: 1 1 auto;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .wrapper__game {
    flex: 1 1 auto;
  }
</style>
