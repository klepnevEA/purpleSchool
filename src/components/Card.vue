<script setup>
    import { ref } from "vue";
    import CloseIcon from "./ui/icons/CloseIcon.vue";
    import CheckIcon from "./ui/icons/CheckIcon.vue";
    const isTurnOf = ref(false);
    const trayGuess = ref(false);
    const isGuess = ref(false);

    const tuonOfCard = () => {
        isTurnOf.value = !isTurnOf.value;
    }

    const noGuess = () => {
        trayGuess.value = true;
        isGuess.value = false;
    }

        const guess = () => {
        trayGuess.value = true;
        isGuess.value = true;
    }
</script>

<template>
 <div class="card">
        <div class="card__wrapper">
            <div class="card__number">1</div>
            <div class="card__check" v-if="trayGuess">
                <CloseIcon :size=36 v-if="!isGuess"/>
                <CheckIcon :size=36 v-else/>
            </div>
            <div class="card__word" v-if="!isTurnOf">unadmitted</div>
            <div class="card__word" v-else>караван верблюдов</div>
            <div class="card__buttons">
                <div class="card__button" v-if="!isTurnOf" @click="tuonOfCard()">Перевернуть</div>
                <div class="card__buttons-check" v-else>
                        <CloseIcon  @click="noGuess()"/>
                        <CheckIcon  @click="guess()"/>
                </div>
            </div>
        </div>
 </div>
</template>

<style scoped>
.card {
    display: flex;
    align-items: stretch;
    background: var(--card-bg-color);
    box-shadow: var(--shadow-card);
    border-radius: 16px;
    padding: 28px 19px;
    height: 376px;
    width: 250px;
    color: var(--text-color);
}

.card__wrapper {
    position: relative;
    width: 100%;
    border: 1px solid var(--border-color);
    border-radius: 12px;
    display: flex;
   align-items: center;
    justify-content: center;
}

.card__number {
    position: absolute;
    top: 0;
    transform: translateY(-50%);
    padding: 1px;
    left: 16px;
    background: var(--card-bg-color);
    font-size: 14px;
}

.card__buttons {
    position: absolute;
    bottom: 0;
    transform: translate(-50%, 50%);
    padding: 1px;
    left: 50%;
    background: var(--card-bg-color);
    font-size: 14px; 
    cursor: pointer;
}

.card__buttons-check {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: space-between;
    bottom: 0;
    transform: translate(-50%, 50%);
    width: 100px;
    height: 24px;
    padding: 10px;
    left: 50%;
    background: var(--card-bg-color);
    cursor: pointer;
}

.card__check {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 1px;
    background: var(--card-bg-color);
}
</style>
