<template>
    <div class="game__header">
        <div class="game__header-text">
            <img :src="logoSrc" alt="Logo" class="game__logo">
        </div>
        <p class="game__score">Счет: <br> {{ score }}</p>
    </div>
</template>

<script setup>
import { computed } from 'vue';
import logoImage from '@/assets/logo.svg';
import bonusLogoImage from '@/assets/logo-bonus.svg';

const props = defineProps({
    isBonus: Boolean,
    score: Number
});

const logoSrc = computed(() => props.isBonus ? bonusLogoImage : logoImage);
</script>

<style scoped>
.game__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px;
    border: 1px solid;
    border-radius: 20px;
    margin-bottom: 100px;
    min-width: 500px;
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

@media (max-width: 400px) {

    .game__header {
        flex-direction: column;
        min-width: 260px; 
    }

    .game__header-text {
        margin-bottom: 20px;
    }
}
</style>