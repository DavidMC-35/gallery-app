<template>
    <h1>Favorites</h1>
    <GalleryContainer 
        :gallery="favorites" 
        @toggle-favorite="$emit('toggle-favorite', $event)"
    ></GalleryContainer>
</template>

<script setup>
import GalleryContainer from '../components/gallery/GalleryContainer.vue';

defineProps({
    favorites: {
        type: Array,
        required: true
    }
});

defineEmits(['toggle-favorite']);
</script>