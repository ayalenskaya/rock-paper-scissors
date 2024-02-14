<template>
    <div class="modal" v-if="isOpen">
        <div class="modal__content">
            <h2>Правила игры</h2>
            <p> Если игрок побеждает, он получает 1 очко. Если компьютер выигрывает, игрок теряет 1 очко.

            <h2>Оригинал</h2>
            <li>Бумага побеждает камень</li>
            <li> Камень побеждает ножницы</li>
            <li> Ножницы побеждают бумагу</li>

            <h2>Бонус</h2>
            <li>Ножницы побеждают бумагу</li>
            <li> Бумага побеждает камень</li>
            <li> Рок побеждает Ящерицу</li>
            <li> Ящерица побеждает Спока</li>
            <li> Спок побеждает Ножницы</li>
            <li> Ножницы побеждают Ящерицу</li>
            
            








 </p>
            <button class="modal__close" @click="closeModal">Закрыть</button>
        </div>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';

const props = defineProps({
    isOpen: Boolean,
});

const emit = defineEmits(['close']);

const closeModal = () => {
    emit('close');
};
</script>
  
<style scoped>
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal__content {
    background: #fff;
    color: #000;
    padding: 20px;
    border-radius: 5px;
}

.modal__close {
    margin-top: 20px;
}
</style>