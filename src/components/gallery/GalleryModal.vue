<template>
    <div v-if="isOpen" class="modal">
        <button @click="closeModal" class="close-btn">
            <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24">
                <path fill="#ffffff" d="M6.4 19L5 17.6l5.6-5.6L5 6.4L6.4 5l5.6 5.6L17.6 5L19 6.4L13.4 12l5.6 5.6l-1.4 1.4l-5.6-5.6z"/>
            </svg>
        </button>
        <div class="modal-content">
            <slot></slot>
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
.modal{
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    height: auto;
    min-height: 400px;
    width: auto;
    min-width: 550px;
    padding: 20px;
    border-radius: 12px;
    /* background-color: #222 ; */
    z-index: 9999;
    backdrop-filter: blur(16px) saturate(180%);
    -webkit-backdrop-filter: blur(16px) saturate(180%);
    background-color: rgba(0, 0, 0, 0.75);
    border: 1px solid rgba(255, 255, 255, 0.125);
}

.modal-content{
    padding: 10px;
    margin-top: 20px;
}

.modal-content h2{
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

.upload-options{
    display: flex;
    gap: 10px;
    padding: 5px 10px;
}

.upload-options button{
    background-color: transparent;
    border: none;
    outline: none;
    padding: 5px;
    color: #ffffff;
}

.file-option:hover{
    border-radius:5px ;
    background-color: rgba(211, 211, 211, 0.195);
}

.file-option:focus{
    border-bottom: 1px solid white;
}

.file-section{
    padding: 25px 20px;
    /* background-color: #c2b5b5; */
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px;
}

#description{
    width: 400px; 
    height: 200px; 
    resize: none;
    border-radius: 8px;
    background-color: rgba(255, 255, 255, 0.1);
    color: white;
    padding: 10px;
}

.field-data{
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px 0;
    padding: 15px;
    display: flex;
    justify-content: center;
    align-items: start;
    gap: 10px;
    flex-direction: column;
    /* margin-bottom: 15px; */
}

.field-data label{
    color: white;
}
</style>