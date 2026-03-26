<script setup>
  import Button from "./components/ui/Button.vue";
  import Main from "./components/Main.vue";
  import Head from "./components/Head.vue";
  import { ref, provide} from "vue";

  const API = 'http://localhost:8080/api/random-words';

  const isGameStart = ref(false);
  const startGame = () => {
    isGameStart.value = !isGameStart.value;
    getWords();
  };

  const count = ref(10);
  const cardsList = ref([]);

  const getWords = async () => {
    try {
      const res = await fetch(API);
      if (!res.ok) {
        throw new Error(`HTTP error! status: ${res.status}`);
      }

      const data = await res.json();

      cardsList.value = data.map(item => ({
        word: item.word,
        translation: item.translation,
        state: "closed",
        status: "pending"
      }));
    } catch (error) {
      console.error("Ошибка при получении слов:", error);
    }
  };

  const handleCardEvent = (cardIndex, cardAction) => {
    if (cardIndex < 0 || cardIndex >= cardsList.value.length) return;

    const card = cardsList.value[cardIndex];
    if (cardAction === 'turnOf') card.state = 'opened';
    else if (cardAction === 'noGuess' && card.status === 'pending') card.status = 'fail';
    else if (cardAction === 'guess' && card.status === 'pending') card.status = 'success';
    };

  provide("count", count);
  provide('cardsList', cardsList);
  provide('cardEvent', handleCardEvent);
</script>

<template>
<div class="wrapper">
  <Head class="wrapper__head" />
  <div class="wrapper__content" v-if="!isGameStart">
    <Button @click="startGame()">Начать игру</Button>
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
