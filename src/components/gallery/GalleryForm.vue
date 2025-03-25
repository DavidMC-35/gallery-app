<template>
    <h2>Agregar Imagen</h2>
    <div class="file-section">
        <div class="upload-options">
            <button class="file-option" @click="handleUploadFile('subir')">Subir</button>
            <button class="file-option" @click="handleUploadFile('insertar')">Insertar Enlace</button>
            </div>
        <div>
            <input v-if="fileOption === 'subir'" type="file">
            <input v-else type="text" placeholder="Insertar enlace aquí">
        </div>
    </div>

    <div class="field-data">
        <label for="">Descripcion</label>
        <textarea name="" id="description"></textarea>
    </div>
    
    <div class="field-data">
        <label for="">Autor</label>
        <input type="text">
    </div>

    <div class="">
        <button @click="closeModal">Cerrar</button>
        <button>Agregar</button>
    </div>
</template>

<script setup>

import { ref } from "vue";
import { defineEmits } from "vue"

const emit = defineEmits(['newImage'])

const fileOption = ref("")
const imagePreview = ref(null);
const selectedFile = ref(null);

const handleUploadFile = (type) => {
    fileOption.value = type; 
}
const handleFileUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
        selectedFile.value = file;
        imagePreview.value = URL.createObjectURL(file);
    }
};

const closeModal = () => {
    emit('close');
};

const submitImage = () => {
    if(selectedFile){
        emit("newImage", selectedFile)
        imagePreview.value = null
    }
}

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
    width: 400px; 
    height: 200px; 
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

/* .form-container {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f5f5f5; 
}

.form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
    padding: 20px;
    background-color: white;
    border-radius: 12px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1); 
    width: 100%;
    max-width: 400px; 
}

.form h2 {
    margin: 0;
    font-size: 1.5rem;
    color: #333;
}

input[type="file"] {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: 100%;
    cursor: pointer;
    transition: border-color 0.3s;
}

input[type="file"]:hover {
    border-color: #888;
}

.image-preview {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    width: 100%;
}

.image-preview img {
    max-width: 100%;
    border-radius: 8px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

button {
    padding: 12px 20px;
    border-radius: 8px;
    border: none;
    background-color: crimson;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
    width: 100%;
}

button:hover {
    background-color: darkred;
    transform: translateY(-2px); 
}

button:active {
    transform: translateY(0); 
} */
</style>