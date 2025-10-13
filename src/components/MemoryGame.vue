<script setup>
import MemoryCard from './MemoryCard.vue';

const cards = [
    { id: 1, card: '🍎' },
    { id: 2, card: '🍌' },
    { id: 3, card: '🍇' },
    { id: 4, card: '🍉' },
    { id: 5, card: '🍓' },
    { id: 6, card: '🍒' },
    { id: 7, card: '🥝' },
    { id: 8, card: '🍍' },
    { id: 9, card: '🥑' },
    { id: 10, card: '🥥' },
];

function shuffleArray(array) {
    array = [...array, ...array];

    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }

    return array;
}

const shuffledCards = shuffleArray(cards);
</script>

<template>
    <section id="game">
        <h2>Let's play!</h2>
        <div class="grid">
            <MemoryCard v-for="card in shuffledCards" :key="card.id" :idCard="card.id">
                <template #content>
                    <span>{{ card.card }}</span>
                </template>
            </MemoryCard>
        </div>
    </section>
</template>

<style>
.grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 10px;
}
</style>