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
        ></GalleryImage>
    </div>
</div>
</template>

<script setup>

    import { defineProps } from 'vue';
    import GalleryImage from './GalleryImage.vue'

    const props = defineProps({
        gallery: Array
    })




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
</style>