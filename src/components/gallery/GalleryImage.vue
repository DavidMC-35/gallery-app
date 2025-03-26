<template>
    <div class="gallery-card">
        <img :src="file" alt="" class="card-image">
        <div class="card-content">
            <h3 class="card-title">{{ description }}</h3>
            <p class="author">Autor: {{ author }}</p>
        </div>
    </div>
</template>

<script setup>
    import { defineProps } from 'vue';
    const props = defineProps({
    id: {
        type: Number,
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
    })

</script>

<style scoped>

.gallery-card {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

    .gallery-card:hover {
        transform: translateY(-5px);
        box-shadow: 0 6px 12px rgba(0,0,0,0.15);
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

.gallery-image {
    width: 100%;
    height: 200px;
    object-fit: cover; 
    border-bottom: 1px solid #ddd;
}

.card-info {
    padding: 15px;
    text-align: center;
}

.author {
    font-size: 0.9rem;
    color: #777;
}

.card-content {
    padding: 15px;
}

.card-title {
    margin: 0 0 5px 0;
    font-size: 1rem;
}

.card-meta {
    display: flex;
    justify-content: space-between;
    color: var(--light-text);
    font-size: 0.8rem;
}

</style>