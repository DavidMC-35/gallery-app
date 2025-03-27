<template>
    <div class="gallery-container">
        <div class="gallery-grid">
            <GalleryImage 
                v-for="(item, index) in gallery"
                :key="index"
                :id="item.id"
                :date="item.date"
                :file="item.file"
                :description="item.description"
                :author="item.author"
                :option="item.option"
                :favorite="item.favorite"
                @open-modal="openModal"
                @toggle-favorite="handleToggleFavorite"
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
    
        import { ref, defineProps, defineEmits } from 'vue';
        import GalleryImage from './GalleryImage.vue'
        import GalleryModal from './GalleryModal.vue'

        const emit = defineEmits(['toggle-favorite']);
        
        const isModalOpen = ref(false);
        const selectedImage = ref({
            file: '',
            description: '',
            author: ''
        });
        
        const props = defineProps({
            gallery: {
                type: Array,
                required: true
            }
        });
    
        const openModal = (image) => {
            selectedImage.value = image;
            isModalOpen.value = true;
        };

        // Modificar esta función para emitir el evento al componente padre
        const handleToggleFavorite = (imageId) => {
            emit('toggle-favorite', imageId);
        };

        // Eliminar o modificar la función addFavorite que no se está usando correctamente
    </script>
    
<style scoped>
.gallery-container {
    width: 100%;
}

.gallery-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr); 
    gap: 15px;
    padding: 20px;
}

.modal-image-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0;
    
}

.modal-image {
    width: 100%;
    max-height: 65vh;
    object-fit: contain;
    border-radius: 8px;
    margin-bottom: 15px;
}

.modal-image-info {
    width: 100%;
    padding: 15px;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 8px;
    margin-top: 0;
}

.modal-image-info h3 {
    margin-bottom: 10px;
    color: #fff;
    font-size: 1.2rem;
}
.modal-image-info p {
    color: #fff;
    font-size: 1rem;
}


    </style>