<template>
    <div class="gallery-card">
        <img :src="file" alt="" class="card-image">
        <div class="card-content">
            <h3 class="card-title">{{ description }}</h3>
            <p class="author">Autor: {{ author }}</p>
        </div>
        <div class="card-menu">
            <button class="menu-btn" :class="{ 'active': isActive }" @click="toggleActive">
                <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24">
                    <path fill="currentColor" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2c-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/>
                </svg>
            </button>
            <!-- <button class="menu-btn" :class="{ 'active': isActive }" @click="toggleActive">
                <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#ffffff" d="m18.988 2.012l3 3L19.701 7.3l-3-3zM8 16h3l7.287-7.287l-3-3L8 13z"/><path fill="#ffffff" d="M19 19H8.158c-.026 0-.053.01-.079.01c-.033 0-.066-.009-.1-.01H5V5h6.847l2-2H5c-1.103 0-2 .896-2 2v14c0 1.104.897 2 2 2h14a2 2 0 0 0 2-2v-8.668l-2 2z"/></svg>
            </button> -->
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const isActive = ref(false);

const toggleActive = () => {
    isActive.value = !isActive.value;
}

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
    }
})
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
</style>