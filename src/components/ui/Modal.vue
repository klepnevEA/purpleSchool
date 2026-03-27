<script setup>
const emit = defineEmits(['close'])
    
    const close = () => {
        emit('close')
    }
</script>

<template>
    <teleport to="body">
        <div class="modal"> 
            <div class="modal__content">
                <div class="modal__close" @click="close()">X</div> 
                <slot />
            </div>
        </div>
    </teleport>
 <div></div>
</template>

<style scoped>
.modal {
    position: fixed;
    display: flex;
    justify-content: center;
    align-items: center;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0,0,0,0.1);
}

.modal__content {
    position: relative;
    background-color: var(--bg-color);
    padding: 20px;
    min-width: 200px;
    border-radius: 16px;
    color: var(--text-color);
}

.modal__close {
    position: absolute;
    top: 0;
    right: 0;
    transform: translate(0, -150%);
    width: 30px;
    height: 30px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;  
    background-color: var(--bg-color);  
    cursor: pointer;
}
</style>
