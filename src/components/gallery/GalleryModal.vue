<template>
    <div v-if="isOpen" class="modal-container">
        <div class="modal-backdrop"></div>
        <div class="modal">
            <button @click="closeModal" class="close-btn">
                <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24">
                    <path fill="#ffffff" d="M6.4 19L5 17.6l5.6-5.6L5 6.4L6.4 5l5.6 5.6L17.6 5L19 6.4L13.4 12l5.6 5.6l-1.4 1.4l-5.6-5.6z"/>
                </svg>
            </button>
            <div class="modal-content">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue';

const props = defineProps({
    isOpen: {
        type: Boolean,
        required: true,
    },
});

const emit = defineEmits(['close']);

const closeModal = () => {
    emit('close');
};
</script>

<style scoped>
.modal-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9998;
}

.modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    backdrop-filter: blur(16px) saturate(180%);
    -webkit-backdrop-filter: blur(16px) saturate(180%);
    background-color: rgba(0, 0, 0, 0.75);
    z-index: 9998;
    animation: fadeIn 0.3s ease-in-out;
}

.modal {
    position: relative;
    height: auto;
    min-height: 400px;
    width: auto;
    min-width: 550px;
    padding: 20px;
    border-radius: 12px;
    background-color: rgba(23, 23, 23, 0.686);
    border: 1px solid rgba(255, 255, 255, 0.125);
    z-index: 9999;
    animation: slideDown 0.4s ease-out;
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

@keyframes slideDown {
    from { 
        opacity: 0;
        transform: translateY(-50px);
    }
    to { 
        opacity: 1;
        transform: translateY(0);
    }
}

.modal-content {
    animation: contentFadeIn 0.2s ease-in-out 0.2s both;
    padding: 10px;
    margin-top: 20px;
}


@keyframes contentFadeIn {
    from { 
        opacity: 0;
        transform: translateY(20px);
    }
    to { 
        opacity: 1;
        transform: translateY(0);
    }
}


.modal-content h2 {
    color: #ffffff;
}

.close-btn {
    border: none;
    outline: none;
    border-radius: 8px;
    background-color: rgb(251, 15, 62);
    position: absolute;
    top: 8px;
    right: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: all 0.3s;
    padding: 8px;
}

.close-btn:hover svg {
    transform: rotate(90deg);
    transition: all 0.3s;
}

.close-btn svg {
    height: 20px;
    width: 20px;
    transition: all 0.3s;
}

.upload-options {
    display: flex;
    gap: 10px;
    padding: 5px 10px;
}

.upload-options button {
    background-color: transparent;
    border: none;
    outline: none;
    padding: 5px;
    color: #ffffff;
}

.file-option:hover {
    border-radius: 5px;
    background-color: rgba(211, 211, 211, 0.195);
}

.file-option:focus {
    border-bottom: 1px solid white;
}

.file-section {
    padding: 25px 20px;
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px;
}

#description {
    width: 400px; 
    height: 200px; 
    resize: none;
    border-radius: 8px;
    background-color: rgba(255, 255, 255, 0.1);
    color: white;
    padding: 10px;
}

.field-data {
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px 0;
    padding: 15px;
    display: flex;
    justify-content: center;
    align-items: start;
    gap: 10px;
    flex-direction: column;
}

.field-data label {
    color: white;
}
</style>