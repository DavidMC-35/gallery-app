<template>
    <div class="title-section">
        <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#f0d000" d="M17.562 21.56a1 1 0 0 1-.465-.116L12 18.764l-5.097 2.68a1 1 0 0 1-1.45-1.053l.973-5.676l-4.124-4.02a1 1 0 0 1 .554-1.705l5.699-.828l2.549-5.164a1.04 1.04 0 0 1 1.793 0l2.548 5.164l5.699.828a1 1 0 0 1 .554 1.705l-4.124 4.02l.974 5.676a1 1 0 0 1-.985 1.169Z"/></svg>
        <h2>Favorites</h2>
    </div>
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

<style scoped>
    .title-section {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 20px 0;
        gap:10px;
        color: #3b9e67; 
    }
    
    .title-section h2{
        border-bottom: 2px solid #ffff;
    }
</style>