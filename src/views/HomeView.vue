<template>
    <div class="title-section">
        <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><g fill="none"><path fill-rule="evenodd" clip-rule="evenodd" d="M5 9a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v3a2 2 0 0 1-2 2H5zm0 13a2 2 0 0 1-2-2v-8a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H5zm10 0a2 2 0 0 1-2-2v-2a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2a2 2 0 0 1-2 2h-4zm0-8a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2h-4z" fill="#ffffff"/></g></svg>
        <h2>Gallery</h2>
    </div>
    <GalleryContainer 
        :gallery="gallery"
        @toggle-favorite="$emit('toggle-favorite', $event)"
    ></GalleryContainer>
</template>

<script setup>
import GalleryContainer from '../components/gallery/GalleryContainer.vue';

defineProps({
    gallery: {
        type: Array,
        required: true
    }
});

defineEmits(['toggle-favorite']);
</script>

<style scoped>
    .title-section {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 20px 0;
        gap: 10px;
        color: #3b9e67; 
    }
    .title-section h2{
        border-bottom: 2px solid #ffff;
    }
</style>