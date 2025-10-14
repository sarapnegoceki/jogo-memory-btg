<script setup>
const emit = defineEmits(['update:startNewGame']);
</script>

<template>
    <section>
        <div class="center">
            <h2>You finish the Game! Do you want restart?</h2>
            <button @click="$emit('update:startNewGame')">Restart Game</button>
        </div>
    </section>
</template>

<style scoped>
    .center{
        text-align: center;
    }
    button{
        background-color: #191cc2;
        color: white;
        border: none;
        border-radius: 5px;
        padding: 10px 15px;
        font-size: 16px;
        cursor: pointer;
        margin-top: 20px;
    }
</style>