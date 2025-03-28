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
                :profileImg="item.profileImg" 
                :option="item.option"
                :favorite="item.favorite"
                @open-modal="openModal"
                @toggle-favorite="handleToggleFavorite" 
            ></GalleryImage>

            <div class="message" v-if="gallery.length === 0">
                <p>No hay imágenes para mostrar.</p>
            </div>
            
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
    
    import { ref, defineProps, defineEmits, watch } from 'vue';
    import GalleryImage from './GalleryImage.vue'
    import GalleryModal from './GalleryModal.vue'

    const emit = defineEmits(['toggle-favorite']);
    
    const isModalOpen = ref(false);
    // const showInfo = ref(false);
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

    const handleToggleFavorite = (imageId) => {
        emit('toggle-favorite', imageId);
    }; 
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
    animation: imageZoomIn 0.6s ease-out;
}

.modal-image-info {
    width: 100%;
    padding: 15px;
    background-color: rgba(242, 242, 242, 0.9);
    border-radius: 8px;
    margin-top: 0;
    animation: slideUp 0.5s ease-out 0.3s both;
}

@keyframes imageZoomIn {
    from {
        opacity: 0;
        transform: scale(0.8);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}

@keyframes slideUp {
    from {
        opacity: 0;
        transform: translateY(10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
.modal-image-info h3 {
    margin-bottom: 10px;
    color: black;
    font-size: 1.2rem;
}
.modal-image-info p {
    color: black;
    font-size: 1rem;
}

.message {
    width: 100%;
    text-align: center;
    color: #fff;
    font-size: 1.2rem;
    /* padding: 20px; */
}

.slide-fade-enter-active, .slide-fade-leave-active {
    transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
}

.slide-fade-enter-from {
    opacity: 0;
    transform: translateY(20px); 
}

.slide-fade-leave-to {
    opacity: 0;
    transform: translateY(-20px); 
}
    

</style>