<script setup>
import { ref } from 'vue';

const count = ref(0);
const props = defineProps({
    idCard: String
});
const emit = defineEmits(['update:score']);

function showCard(event) {
    const card = event.target.closest('.card');

    const front = card.querySelector('.card-front');
    front.classList.toggle('show');

    compareCards({id: card.id, content: front.textContent.trim()});
}

function compareCards(card){
    const lastCard = localStorage.getItem('lastCard') ? JSON.parse(localStorage.getItem('lastCard')) : {id: null, content: null};

    if(lastCard.id === null && lastCard.content === null) {
        lastCard.id = card.id;
        lastCard.content = card.content;
        localStorage.setItem('lastCard', JSON.stringify(lastCard));
    } else {
        if(lastCard.content === card.content && lastCard.id !== card.id){
            emit('update:score');
        } else {
            setTimeout(() => {
                const lastCardElement = document.getElementById(lastCard.id);
                const currentCardElement = document.getElementById(card.id);

                if(lastCardElement && currentCardElement){
                    lastCardElement.querySelector('.card-front').classList.remove('show');
                    currentCardElement.querySelector('.card-front').classList.remove('show');
                }
            }, 1000);
        }

        localStorage.removeItem('lastCard');
    }
}
</script>

<template>
    <div class="card" @click="showCard($event)" :id="props.idCard">
        <div class="card-inner">
            <div class="card-front">
                <slot name="content"></slot>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .card{
        width: 100px;
        height: 100px;
        background: #a0a0a0;
        display: block;
        border-radius: 10px;
    }
    .card .card-inner{
        height: 100%;
    }
    .card .card-front.show{
        display: flex;
    }
    .card-front{
        display: none;
        justify-content: center;
        align-items: center;
        align-content: center;
        height: 100%;
    }
</style>