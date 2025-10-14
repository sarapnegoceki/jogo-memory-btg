<script setup>
import { ref } from 'vue';

const emit = defineEmits(['update:setPlayerName']);
const playerName = ref(localStorage.getItem('player') || '');

function setPlayerName() {
    localStorage.setItem('player', playerName.value);
    emit('update:setPlayerName');
}
</script>

<template>
    <div>
        <form @submit.prevent="setPlayerName()">
            <label for="player">What's your name?</label>
            <input type="text" name="player" id="player" v-model="playerName">
            <button type="submit">Start</button>
        </form>
    </div>
</template>

<style scoped>
    label {
        font-size: 20px;
        font-weight: bold;
        color: black;
        margin-bottom: 10px;
        display: block;
    }
    input#player {
        border: 1px solid #636363;
        border-radius: 5px;
        padding: 10px;
        font-size: 16px;
        width: 200px;
        display: inline-block;
    }
    button{
        background-color: #191cc2;
        color: white;
        border: none;
        border-radius: 5px;
        padding: 10px 15px;
        font-size: 16px;
        cursor: pointer;
        margin-left: 10px;
        display: inline-block;
    }
</style>