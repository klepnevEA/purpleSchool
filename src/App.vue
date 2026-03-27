<script setup>
  import Button from "./components/ui/Button.vue";
  import Main from "./components/Main.vue";
  import Head from "./components/Head.vue";
  import Modal from './components/ui/Modal.vue';
  import { ref, provide, computed, watch} from "vue";

  const API = 'http://localhost:8080/api/random-words';

  const isGameStart = ref(false);
  const startGame = () => {
    isGameStart.value = !isGameStart.value;
    getWords();
  };

  const newGame = () => {
    count.value = 0;
    isShowModal.value = false;
    cardsCount.value = 0;
    getWords();
  };

  const count = ref(0);
  const cardsCount = ref(0);
  const cardsList = ref([]);
  const POINT_CUCCESS = 10;
  const POINT_FAIL = 4;
  const isShowModal = ref(false);
  const isVictory = ref(false);

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
    else if (cardAction === 'noGuess' && card.status === 'pending') {
      cardsCount.value++;
      card.status = 'fail';
      if(count.value <= 0 ) {
        count.value = 0
      } else {
        count.value = count.value - POINT_FAIL;
      }
    }
    else if (cardAction === 'guess' && card.status === 'pending') {
      cardsCount.value++;
      card.status = 'success';
      count.value = count.value + POINT_CUCCESS;
    }};

    const close = () => {
      isShowModal.value = false;
    }

  provide("count", count);
  provide('cardsList', cardsList);
  provide('cardEvent', handleCardEvent);

  watch(()=> cardsCount.value,
    ()=> {
      if( cardsCount.value == cardsList.value.length) {
        isShowModal.value = true;
        if(count.value  == cardsList.value.length * POINT_CUCCESS) {
          isVictory.value = true
        } else {
          isVictory.value = false
        }
      }
    }
  )

</script>

<template>
<div class="wrapper">

  <Head class="wrapper__head" />
  <div class="wrapper__content" v-if="!isGameStart">
    <Button @click="startGame()">Начать игру</Button>
  </div>
  <Main class="wrapper__game" @newGame="newGame()" v-else />
    <Modal v-if="isShowModal"  @close="close()">
      <div class="result-game">
        <div class="result-game__title">
          {{isVictory ? "Вы победили" : "Вы проиграли" }}
        </div>
        <div class="result-game__message">
          Вы набрали {{count}} очков из {{ cardsList.length * POINT_CUCCESS  }} возмжных.
        </div>
        <div class="result-game_footer">
          <Button @click="newGame()">Начать заново</Button>
        </div>
      </div>
  </Modal>
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

  .footer {
    display: flex;
    justify-content: center;
  }

  .result-game {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;
  }
</style>
