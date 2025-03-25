<template>
    <div v-if="isOpen" class="modal" @click="closeModal">
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
    width: 600px;
    padding: 20px;
    border-radius: 12px;
    background-color: #222 ;
}

.modal-content{
    /* border: 1px solid black; */
    padding: 10px;
}

.modal-content h2{
    color: #ffffff;
}


.upload-options{
    /* background-color: aqua; */
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
    width: 400px; /* Ancho fijo */
    height: 200px; /* Alto fijo */
    resize: none;
    border-radius: 8px;
}

.field-data{
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px;
    padding: 10px 20px;
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