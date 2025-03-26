<template>
    <div class="gallery-container">
        <div class="gallery-grid">
            <GalleryImage
                v-for="(item, index) in gallery"
                :key="item.id"
                :id="item.id"
                :date="item.date"
                :file="item.file"
                :description="item.description"
                :author="item.author"
                :option="item.option"
                @open-modal="openModal"
            ></GalleryImage>
            <GalleryModal 
                :isOpen="isModalOpen"
                @close="isModalOpen = false">
                <div class="modal-image-container">
                    <img :src="selectedImage.file" alt="Imagen en grande" class="modal-image" />
                    <div class="modal-image-info">
                        <h3>{{ selectedImage.description }}</h3>
                        <p>Autor: {{ selectedImage.author }}</p>
                    </div>
                </div>
            </GalleryModal>
        </div>
    </div>
    </template>
    
    <script setup>
    
        import { ref, defineProps } from 'vue';
        import GalleryImage from './GalleryImage.vue'
        import GalleryModal from './GalleryModal.vue'
    
        const isModalOpen = ref(false);
        const selectedImage = ref({
            file: '',
            description: '',
            author: ''
        });
        const props = defineProps({
            gallery: Array
        })
    
        const openModal = (image) => {
            selectedImage.value = image;
            isModalOpen.value = true;
        };
    
    </script>
    
<style scoped>
.gallery-container {
    width: 100%;
}

.gallery-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr); 
    gap: 10px;
    padding: 20px;
}

.modal-image-container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.modal-image {
    width: 100%;
    height: auto;
    max-height: 70vh;
    object-fit: contain;
    border-radius: 8px;
}

.modal-image-info {
    margin-top: 10px;
    color: white;
    text-align: center;
    width: 100%;
}

.modal-image-info h3 {
    margin-bottom: 5px;
}
    </style>