<template>
    <h2>Agregar Imagen</h2>
    <form @submit.prevent="submitForm">
        <div class="file-section">
            <div class="upload-options">
                <button type="button" class="file-option" @click="handleUploadFile('subir')">Subir</button>
                <button type="button" class="file-option" @click="handleUploadFile('insertar')">Insertar Enlace</button>
                </div>
            <div>
                <input v-if="fileOption === 'subir'" type="file" @change="handleFileChange">
                <input v-else v-model="imageURL" type="text" placeholder="Insertar enlace aquí">
            </div>
        </div>

        <div class="field-data">
            <label for="">Descripcion</label>
            <textarea name="" v-model="description" id="description"></textarea>
        </div>
        
        <div class="field-data">
            <label for="">Autor</label>
            <input v-model="author" type="text">
        </div>

        <div>
            <button @click="closeModal" class="btn" id="close-btn"><svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#ffffff" d="M6.4 19L5 17.6l5.6-5.6L5 6.4L6.4 5l5.6 5.6L17.6 5L19 6.4L13.4 12l5.6 5.6l-1.4 1.4l-5.6-5.6z"/></svg></button>
            <button type="submit">Subir</button>
        </div>
    </form>
</template>

<script setup>

import { ref } from "vue";
import { defineEmits } from "vue"

const emit = defineEmits(['newImage','close'])

const fileOption = ref(""); 
const selectedFile = ref(null); 
const imageURL = ref(""); 
const description = ref(""); 
const author = ref("");
const errors = ref(false) 

const closeModal = () => {
    emit('close');
};

const handleUploadFile = (option) => {
    fileOption.value = option
}

const handleFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    selectedFile.value = file;
    imageURL.value = URL.createObjectURL(file); // Genera una URL temporal para la imagen
  }
};

const submitForm = () => {
    const uniqueId = Date.now(); 
    const currentDate = new Date().toLocaleDateString()

    if (!fileOption.value) {
        alert("Por favor, selecciona si subirás una imagen o insertarás un enlace.");
        return;
    }

    if (fileOption.value === "subir" && !selectedFile.value) {
        alert("Por favor, selecciona un archivo.");
        return;
    }

    if (fileOption.value === "insertar" && !imageURL.value.trim()) {
        alert("Por favor, introduce un enlace válido.");
        return;
    }
    
    if (!description.value.trim()) {
        alert("La descripción no puede estar vacía.");
        return;
    }

    if (!author.value.trim()) {
        alert("El autor no puede estar vacío.");
        return;
    }

    const imageSrc = fileOption.value === "subir" 
        ? URL.createObjectURL(selectedFile.value)  
        : imageURL.value; 

    emit("newImage", {
        id:uniqueId,
        date: currentDate,
        file: imageSrc,
        description: description.value,
        author: author.value,
        option:fileOption.value,    
        })
        
        selectedFile.value = null;
        imageURL.value = "";
        description.value = "";
        author.value = "";
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

.btn{
    padding: 5px 10px;
    background-color: #3b9e67;
    border-radius: 12px;
    border: none;
    margin: 5px;
    cursor: pointer;
}

#close-btn{
    background-color: tomato;
    position: absolute;
    top: 10px;
    right: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.3s;
}

#close-btn:hover svg{
    transform: translateY(-2px);
    transition: all 0.3s;

}

#close-btn svg{
    height: 25px;
    width: 25px;
    transition: all 0.3s;

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