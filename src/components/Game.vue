<template>
    <div class="game">
        <div class="game__header">
            <div class="game__header-text">
                <h1 class="game__header-title">rock</h1>
                <h1 class="game__header-title">paper</h1>
                <h1 class="game__header-title">scissors</h1>
            </div>
            <p class="game__score">Счет: <br> {{ score }}</p>
        </div>
        <div v-if="!userChoice && !computerChoice" class="game__choices">
            <button class="game__choice-button game__choice-button--paper" @click="play('paper')">
                <img class="game__choice-image" src="@/assets/paper.svg" alt="Бумага" />
            </button>
            <button class="game__choice-button game__choice-button--scissors" @click="play('scissors')">
                <img class="game__choice-image" src="@/assets/scissors.svg" alt="Ножницы" />
            </button>
            <button class="game__choice-button game__choice-button--rock" @click="play('rock')">
                <img class="game__choice-image" src="@/assets/rock.svg" alt="Камень" />
            </button>
            
          
        </div>
        <div class="game__results" v-if="userChoice && computerChoice">
            <div class="game__result-item">
                <h1 class="game__result-title">Вы выбрали</h1>
                <div class="game__result-image"
                :class="`game__result-image--${userChoice}`">
                    <img :src="`src/assets/${userChoice}.svg`" :alt="`Вы выбрали ${userChoice}`" />
                </div>
            </div>
            <div class="game__result-item">
                <span class="game__result-text">
                    <p>{{ result }}</p>
                </span>
                <button class="game__play-again-button" v-if="result" @click="resetGame">
                    Играть снова
                </button>
            </div>
            <div class="game__result-item">
                <h1 class="game__result-title">Компьютер выбрал</h1>
                <div class="game__result-image"
                :class="`game__result-image--${computerChoice}`">
                    <img :src="`src/assets/${computerChoice}.svg`" :alt="`Компьютер выбрал ${computerChoice}`" />
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { ref, onBeforeUnmount } from 'vue';

const score = ref(parseInt(localStorage.getItem('score')) || 0);
const result = ref('');
const userChoice = ref(null);
const computerChoice = ref(null);

const play = (choice) => {
    const choices = ['rock', 'paper', 'scissors'];
    const computerChoiceValue = choices[Math.floor(Math.random() * choices.length)];

    userChoice.value = choice;
    computerChoice.value = computerChoiceValue;

    if (choice === computerChoiceValue) {
        result.value = 'Ничья!';
    } else if (
        (choice === 'rock' && computerChoiceValue === 'scissors') ||
        (choice === 'paper' && computerChoiceValue === 'rock') ||
        (choice === 'scissors' && computerChoiceValue === 'paper')
    ) {
        result.value = 'Вы победили!';
        score.value++;
    } else {
        result.value = 'Вы проиграли!';
        score.value--;
    }

    saveScore();
};

const saveScore = () => {
    localStorage.setItem('score', score.value);
};

const resetGame = () => {
    userChoice.value = null;
    computerChoice.value = null;
    result.value = '';
};

 
window.addEventListener('beforeunload', saveScore);

 
onBeforeUnmount(() => {
    window.removeEventListener('beforeunload', saveScore);
});
</script>
  
<style scoped>
 
.game {
    text-align: center; 
}

.game__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px;
    border: 1px solid;
    border-radius: 20px;
    margin-bottom: 100px;
}

.game__header-text {
    text-align: start;
}

.game__header-title {
    margin: 0;
    font-size: 30px;
}

.game__score {
    margin: 0;
    padding: 10px 20px;
    background-color: #fff;
    color: #192042;
    font-size: 30px;
    font-weight: 700;
    border-radius: 20px;
}

.game__choices {
    margin-top: 20px;
    width: 500px;
    background-image: url('@/assets/bg-triangle.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain; 
}

.game__choice-button {
    margin: 0 10px; 
    border: 20px solid;
    border-radius: 50%;
    width: 150px;
    height: 150px;
}

.game__choice-button--rock {
    border: 20px solid coral; 
}

.game__choice-button--paper { 
    border: 20px solid blue;
    position: relative;
    top: -50px;
    left: -50px;
}

.game__choice-button--scissors {
    border: 20px solid gold;
    position: relative;
    top: -50px;
    left: 50px;
}
 

.game__results {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    gap: 20px;
}

.game__result-item {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.game__result-title {
    margin: 20px 0;
    font-size: 20px;
}

.game__result-image {
    height: 200px;
    width: 200px; 
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #fff;
    color: #000;
}

.game__result-image--rock {
  border: 20px solid coral;
}

.game__result-image--paper {
    border: 20px solid blue;
}

.game__result-image--scissors {
    border: 20px solid gold;
}
.game__result-text {
    margin: 10px 0;
}

.game__play-again-button {
    margin-top: 10px;
}

@media (max-width: 600px) {
    .game {
        margin-top: 20px;
    }

    .game__header {
        flex-direction: column;
    }

    .game__header-text {
        margin-bottom: 20px;
    }

    .game__choices { 
        width: 100%;
    }

    .game__choice-button {
        width: 100px;
        height: 100px;
    }

    .game__choice-button--rock, .game__choice-button--paper, .game__choice-button--scissors {
    border-width: 10px; 
}
 

    .game__results {
        flex-direction: column;
    }

    .game__result-image {
        width: 100px;
        height: 100px;
    }
}

</style>