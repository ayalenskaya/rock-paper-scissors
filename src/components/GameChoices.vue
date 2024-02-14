<template>
    <div v-if="!userChoice && !computerChoice" class="game__choices">
        <button class="game__choice-button game__choice-button--paper" @click="$emit('play', 'paper')">
            <img class="game__choice-image" src="@/assets/paper.svg" alt="Бумага" />
        </button>
        <button class="game__choice-button game__choice-button--scissors" @click="$emit('play', 'scissors')">
            <img class="game__choice-image" src="@/assets/scissors.svg" alt="Ножницы" />
        </button>
        <button class="game__choice-button game__choice-button--rock" @click="$emit('play', 'rock')">
            <img class="game__choice-image" src="@/assets/rock.svg" alt="Камень" />
        </button>
    </div>
</template>

<script setup>
const emit = defineEmits(['play']);
</script>

<style scoped>
.game__choices {
    margin-top: 20px;
    width: 500px;
    background-image: url('@/assets/bg-triangle.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;
}

@media (max-width: 400px) {

    .game__choices {
        width: 100%;
        margin-bottom: 50px;
    }

    .game__choice-button {
        width: 100px;
        height: 100px;
    }
}
</style>