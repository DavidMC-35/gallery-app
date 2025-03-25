<template>
    <div class="gallery-image">
        <img :src="file" alt="" >
        <div class="info">
            <p>{{ description }}</p>
            <p>{{ author }}</p>
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

    .gallery-image{
        height: auto;
        width: 450px;
        background-color: lightgray;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        border-radius: 12px;
    }

    .gallery-image img{
        height: 350px;
        width: 400px;
    }

</style>