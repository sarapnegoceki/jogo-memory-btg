<script setup>
const props = defineProps({
    idCard: String
});

function showCard(event) {
    const card = event.target.closest('.card');

    const front = card.querySelector('.card-front');
    front.classList.toggle('show');

    compareCards(card.id);
}

function compareCards(card){
    let lastCard = localStorage.getItem('cardInPlay');

    if(!lastCard) {
        localStorage.setItem('cardInPlay', card);
    } else {
        if(lastCard === card){
            console.log('Match!');
        } else {
            console.log('No match!');
            setTimeout(() => {
                const lastCardElement = document.getElementById(lastCard);
                const currentCardElement = document.getElementById(card);

                if(lastCardElement && currentCardElement){
                    lastCardElement.querySelector('.card-front').classList.remove('show');
                    currentCardElement.querySelector('.card-front').classList.remove('show');
                }
            }, 1000);
        }

        localStorage.removeItem('cardInPlay');
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

<style>
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