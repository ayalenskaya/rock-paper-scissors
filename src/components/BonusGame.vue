<template>
    <game-header v-if="isOpen" :isBonus="true" :score="score" />
    <div :class="{ 'bonus-game': true, 'no-background': userChoice }" v-if="isOpen">

        <div class="bonus-game__content">
            <div v-if="!userChoice">
                <button v-for="choice in choices" :key="choice" @click="playBonus(choice)" class="game__choice-button"
                    :class="`game__choice-button--${choice}`">
                    <img :src="`src/assets/${choice}.svg`" :alt="`Выбор ${choice}`" />
                </button>
            </div>
            <game-results v-if="userChoice" :userChoice="userChoice" :computerChoice="computerChoice" :result="result"
                @reset="resetGame" />
        </div>

    </div>
</template>

<script setup>
import { ref } from 'vue';
import GameResults from '@/components/GameResults.vue';
import GameHeader from '@/components/GameHeader.vue';

const props = defineProps({
    isOpen: Boolean,
});

const emit = defineEmits(['close']);

const score = ref(parseInt(localStorage.getItem('bonusScore')) || 0);
const userChoice = ref(null);
const computerChoice = ref(null);
const result = ref('');

const choices = ['paper', 'scissors', 'rock', 'lizard', 'spock'];

const rules = {
    'scissors': ['paper', 'lizard'],
    'paper': ['rock', 'spock'],
    'rock': ['lizard', 'scissors'],
    'lizard': ['spock', 'paper'],
    'spock': ['scissors', 'rock']
};

const playBonus = (choice) => {
    const computerChoiceValue = choices[Math.floor(Math.random() * choices.length)];

    userChoice.value = choice;
    computerChoice.value = computerChoiceValue;

    if (userChoice.value === computerChoice.value) {
        result.value = 'Ничья!';
    } else if (rules[userChoice.value].includes(computerChoice.value)) {
        result.value = 'Вы победили!';
        score.value++;
        localStorage.setItem('bonusScore', score.value);
    } else {
        result.value = 'Вы проиграли!';
        score.value--;
        localStorage.setItem('bonusScore', score.value);
    }
};

const resetGame = () => {
    userChoice.value = null;
    computerChoice.value = null;
    result.value = '';
};

const closeGame = () => {
    emit('close');
    resetGame();
};
</script>
 
  
<style scoped>
.bonus-game {
    background-image: url('@/assets/bg-pentagon.svg');
    width: 500px;
    background-repeat: no-repeat;
    background-position: center;

}

.game__choice-button--paper {
    position: relative;
    top: -16px;
    left: 81px;
}

.game__choice-button--rock {
    left: -96px;
    top: -25px;
}

.game__choice-button--spock {
    top: 0;
    left: -95px;
}

.game__choice-button--lizard {
    top: 154px;
    left: 30px;
}

.game__choice-button--scissors {
    top: 111px;
    left: 90px;
}

.bonus-game.no-background {
    background-image: none;
}

@media (max-width: 400px) {
    .bonus-game {
        width: 300px;
        margin-bottom: 50px;
    }

    .game__choice-button {
        width: 100px;
        height: 100px;
    }

    .game__choice-button--lizard {
        top: 130px;
    }

    .game__choice-button--spock {
        top: 28px;
    }

    .game__choice-button--rock {
        left: -60px;
    }

    .game__choice-button--scissors {
        top: 80px;
        left: 63px;
    }

    .game__choice-button--paper {

        left: 63px;
    }
}
</style> 