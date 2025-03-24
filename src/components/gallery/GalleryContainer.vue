<template>
<div class="gallery-container">
    <div class="gallery-grid">
        <!-- <GalleryImage></GalleryImage> -->
    </div>
</div>
</template>

<script setup>
    import GalleryImage from './GalleryImage.vue'

</script>

<style scoped>
    gallery-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 16px;
    padding: 16px;
    }
</style>