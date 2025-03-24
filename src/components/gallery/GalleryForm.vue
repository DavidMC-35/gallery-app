<template>
    <div class="form-container">
        <form class="form" @submit.prevent="submitImage">
            <h2>Agregar Imagen</h2>
            <input type="file" accept="image/*" @change="handleFileUpload" />
            <div class="image-preview" v-if="imagePreview">
                <h3>Vista previa</h3>
                <img :src="imagePreview" alt="Vista previa" />
            </div>
            <button type="submit">Agregar Imagen</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { defineEmits } from "vue"

const emit = defineEmits(['newImage'])

const imagePreview = ref(null);
const selectedFile = ref(null);

const handleFileUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
        selectedFile.value = file;
        imagePreview.value = URL.createObjectURL(file);
    }
};

const submitImage = () => {
    if(selectedFile){
        emit("newImage", selectedFile)
        imagePreview.value = null
    }
}

</script>

<style scoped>

.form-container {
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
}
</style>