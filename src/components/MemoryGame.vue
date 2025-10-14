<script setup>
import { ref } from 'vue';
import MemoryCard from './MemoryCard.vue';

const cards = [
    { card: '🍎' },
    { card: '🍌' },
    { card: '🍇' },
    { card: '🍉' },
    { card: '🍓' },
    { card: '🍒' },
    { card: '🥝' },
    { card: '🍍' },
    { card: '🥑' },
    { card: '🥥' },
];


function shuffleArray(array) {
    array = [...array, ...array];
    
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
    
    return array;
}

const rounds = ref(0);
const shuffledCards = ref(shuffleArray(cards));
const score = ref(0);
const emit = defineEmits(['update:restartGame']);

function incrementScore(){
    score.value++;

    if(score.value === 10){
        rounds.value = rounds.value + 1;
        score.value = 0;
        shuffledCards.value = shuffleArray(cards);

        const allCards = document.querySelectorAll('.card-front.show');
        allCards.forEach(card => card.classList.remove('show'));

        localStorage.removeItem('lastCard');
        emit('update:restartGame');
    }
}
</script>

<template>
    <section id="game">
        <h2>Let's play!</h2>
        <h3>Rounds: {{ rounds }}</h3>
        <div class="grid">
            <MemoryCard v-for="(card, index) in shuffledCards" :key="index" :idCard="'card' + index" @update:score="incrementScore()">
                <template #content>
                    <span>{{ card.card }}</span>
                </template>
            </MemoryCard>
        </div>
    </section>
</template>

<style scoped>
.grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 10px;
}
</style>