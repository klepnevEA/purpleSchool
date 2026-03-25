<script setup>
  import Button from "./components/ui/Button.vue";
  import Main from "./components/Main.vue";
  import Head from "./components/Head.vue";
  import {ref} from "vue";

  const isGameStart = ref(false);
  const statrGame = () => {
    isGameStart.value = !isGameStart.value
  }
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
