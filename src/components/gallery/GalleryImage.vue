<template>
    <div class="gallery-card" @click="openImageModal">
        <img :src="file" alt="" class="card-image">
        <div class="card-content">
                <h3 class="card-title">{{ description }}</h3>
            <div class="card-info">
                <img :src="profileImg" alt="Autor" class="author-img"> 
                <p class="author">Autor: {{ author }}</p>
            </div>
        </div>
        <div class="card-menu">
            <button class="menu-btn" 
                    :class="{ 'active': favorite }" 
                    @click.stop="toggleFavorite">
                <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24">
                    <path fill="currentColor" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2c-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/> 
                </svg>
            </button>
        </div>
    </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue';

const emit = defineEmits(['open-modal', 'toggle-favorite']);

const props = defineProps({
    id: {
        type: String,
        required: true,
    },
    file: {
        type: String,
        required: true,
    },
    description: {
        type: String,
        required: true,
    },
    author: {
        type: String,
        required: true,
    },
    favorite: {
        type: Boolean,
        default: false
    },
    profileImg: {
        type: String,
        required: true, 
    }
});

const toggleFavorite = (event) => {
    event.stopPropagation();
    emit('toggle-favorite', props.id);
};

const openImageModal = () => {
    emit('open-modal', {
        file: props.file,
        description: props.description,
        author: props.author
    });
};
</script>

<style scoped>

.gallery-card {
    position: relative;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.gallery-card:hover {
    transform: translateY(-5px);
    box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.2);
}

.card-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.card-content {
    padding: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

}

.card-title {
    margin: 0 0 5px 0;
    font-size: 1rem;
    padding: 5px;
    border-left: 5px solid #3b9e67;
}

.card-menu {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 12px;
    right: 20px;
    background-color: #353b3842;
    border-radius: 5px;
    padding: 2px;
}

.menu-btn {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: transparent;
    border: none;
    cursor: pointer;
}

.menu-btn svg {
    height: 20px;
    width: 20px;
    color: #ffffff;
    transition: color 0.3s ease;
}

.menu-btn.active svg {
    color: crimson;
}

.author-img{
    height: 50px;
    width: 50px;
    border-radius: 50%;
    margin: 15px 0;
}

.card-info{
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.slide-fade-enter-active,
.slide-fade-leave-active {
    transition: opacity 0.3s ease;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
    opacity: 0;
}

</style>