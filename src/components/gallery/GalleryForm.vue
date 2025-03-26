<template>
    <h2>Agregar Imagen</h2>
    <form @submit.prevent="submitForm">
        <div class="file-section">
            <svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" viewBox="0 0 24 24"><path fill="#ffffff" d="M0 17.143V24h24v-6.857zm5.143 5.143H1.714v-1.714h3.429zm12-17.143h-3.429v8.571h-3.429V5.143H6.856L11.999 0z"/></svg>
            <div class="upload-options">
                <button type="button" 
                    class="file-option" 
                    :class="{ active: fileOption === 'subir' }" 
                    @click="handleUploadFile('subir')"
                    >Subir
                </button>
                <button type="button" 
                    class="file-option" 
                    :class="{ active: fileOption === 'insertar' }" 
                    @click="handleUploadFile('insertar')"
                    >Insertar Enlace
                </button>
            </div>
            <div>
                <input v-if="fileOption === 'subir'" type="file" @change="handleFileChange">
                <input v-else v-model="imageURL" type="text" placeholder="Insertar enlace aquí">
            </div>
        </div>

        <div class="field-form">
            <div class="field-header">
                <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#ffffff" d="M8 18h8v-2H8zm0-4h8v-2H8zm-2 8q-.825 0-1.412-.587T4 20V4q0-.825.588-1.412T6 2h8l6 6v12q0 .825-.587 1.413T18 22zm7-13h5l-5-5z"/></svg>
                <label for="description">Descripcion</label>
            </div>
            <textarea name="" v-model="description" id="description"></textarea>
        </div>
        
        <div class="field-form">
            <div class="field-header">
                <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#ffffff" d="M17 9c0-1.381-.56-2.631-1.464-3.535C14.631 4.56 13.381 4 12 4s-2.631.56-3.536 1.465C7.56 6.369 7 7.619 7 9s.56 2.631 1.464 3.535C9.369 13.44 10.619 14 12 14s2.631-.56 3.536-1.465A4.98 4.98 0 0 0 17 9M6 19c0 1 2.25 2 6 2c3.518 0 6-1 6-2c0-2-2.354-4-6-4c-3.75 0-6 2-6 4"/></svg>
                <label for="author">Autor</label>
            </div>
            <input v-model="author" type="text" id="author">
        </div>
        
        <div class="form-buttons">
            <button type="submit" id="addBtn">Subir</button>
        </div>
    </form>
</template>

<script setup>

import { ref } from "vue";
import { defineEmits } from "vue"

const emit = defineEmits(['newImage','close'])

const fileOption = ref("subir"); 
const selectedFile = ref(null); 
const imageURL = ref(""); 
const description = ref(""); 
const author = ref("");

const closeModal = () => {
    emit('close');
};

const handleUploadFile = (option) => {
    fileOption.value = option;
    // Si el usuario cambia a "insertar", limpiar el archivo seleccionado
    if (option === "insertar") {
        selectedFile.value = null;
    }
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

.upload-options button{
    background-color: transparent;
    border: none;
    outline: none;
    padding: 5px;
    color: #ffffff;
}
.upload-options {
    display: flex;
    gap: 10px;
    padding: 5px 10px;
}

.file-option {
    background-color: transparent;
    border: none;
    outline: none;
    padding: 5px;
    color: #ffffff;
    cursor: pointer;
    font-weight: bold;
    margin: 5px 0px;
    transition: all 0.3s ease-in-out;
}

.file-option:hover {
    border-radius: 5px;
    background-color: rgba(211, 211, 211, 0.195);
}

.file-option.active {
    background-color: #3b9e67;  
    color: white;
    border-radius: 5px;
    padding: 5px 10px;
    font-weight: bold;
}


.file-section{
    padding: 25px 20px;
    /* background-color: #c2b5b5; */
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px;
}


.field-form{
    border: solid 2px rgba(211, 211, 211, 0.2);
    border-radius: 10px;
    margin: 10px;
    padding: 10px 20px;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.field-header {
    display: flex;
    align-items: center;
    gap: 15px;
    padding: 15px 0px;
}

.field-header svg{
    height: 25px;
    width: 25px;
}

.field-form label{
    color: white;
    font-weight: 500;
}

input[type="text"], 
input[type="file"], 
textarea {
    width: 100%;
    padding: 8px;
    border: 2px solid rgba(211, 211, 211, 0.2); 
    border-radius: 8px;  
    background-color: rgba(255, 255, 255, 0.1); 
    color: white; 
    font-size: 14px;
    outline: none;
    transition: all 0.3s ease-in-out;
    box-sizing: border-box;
}

input[type="text"]:focus, 
input[type="file"]:focus, 
textarea:focus {
    border-color: #3b9e67;  
    background-color: rgba(255, 255, 255, 0.2); 
    box-shadow: 0 0 5px rgba(59, 158, 103, 0.5); 
}

textarea {
    height: 150px;
    resize: none;
}

input::placeholder, 
textarea::placeholder {
    color: rgba(255, 255, 255, 0.5);
}


#close-btn{
    border: none;
    outline: none;
    border-radius: 8px;
    background-color: tomato;
    position: absolute;
    top: 10px;
    right: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: all 0.3s;
}

#close-btn:hover svg{
    /* transform: scale(1.1); */
    transition: all 0.3s;

}

#close-btn svg{
    height: 20px;
    width: 20px;
    transition: all 0.3s;
}

.form-buttons {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    width: 100%;
}

#addBtn{
    margin-top: 10px;
    padding: 10px 12px;
    width: 100%;
    border: none;
    cursor: pointer;
    border-radius: 12px;
    transition: all 0.3s ease-in-out;
    font-weight: bold;
}

#addBtn:hover{
    background-color: #3b9e67;  
    color: #ffffff;
}
</style>