<script setup>
    import { ref,  inject } from "vue";
    import CloseIcon from "./ui/icons/CloseIcon.vue";
    import CheckIcon from "./ui/icons/CheckIcon.vue";
    const props = defineProps(["cardInfo", "id"]);
    const cardEvent = inject('cardEvent');

    const eventClick = (id, action) => {
        cardEvent(props.id, action )
    }
</script>

<template>
 <div class="card">
        <div class="card__wrapper">
            <div class="card__number">{{props.id + 1}}</div>
            <div class="card__check" v-if="props.cardInfo.status != 'pending'">
                <CloseIcon :size=36 v-if="props.cardInfo.status == 'fail'"/>
                <CheckIcon :size=36 v-else/>
            </div>
            <div class="card__word" v-if="props.cardInfo.state == 'closed'">{{props.cardInfo.word}}</div>
            <div class="card__word" v-else>{{props.cardInfo.translation}}</div>
            <div class="card__buttons">
                <div class="card__button" v-if="props.cardInfo.state == 'closed'" @click="eventClick(props.id, 'turnOf')">Перевернуть</div>
                <div class="card__buttons-check" v-else>
                        <CloseIcon @click="eventClick(props.id, 'noGuess')"/>
                        <CheckIcon @click="eventClick(props.id, 'guess')"/>
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
