<script setup>
  import HeadtIcon from "./icons/Heart.vue";
  const props = defineProps(["count"])
</script>


<template>
  <div class="count">{{props.count}} <HeadtIcon :size="'24px'"/></div>
</template>

<style scoped>
.count {
    display: flex;
    align-items: center;
    padding: 12px 24px;
    gap: 10px;
    box-shadow: var(--shadow);
    border-radius: 36px;
    background-color: var(--count-bg-color);
    color: var(--count-color);
    font-weight: 700;
}
</style>
