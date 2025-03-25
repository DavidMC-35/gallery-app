<template>
    <nav class="navbar">
        <div class="navbar-logo">
            <h1>Dashboard</h1>
        </div>
        <ul class="navbar-links">
            <li><a href="#home">Inicio</a></li>
            <li><a href="#gallery">Editar</a></li>
        </ul>

        <div class="navbar-options">
            <button class="navbar-button" @click="handleAddImage"><svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#ffffff" d="M20.987 16a1 1 0 0 0-.039-.316l-2-6A1 1 0 0 0 18 9h-4v2h3.279l1.667 5H5.054l1.667-5H10V9H6a1 1 0 0 0-.948.684l-2 6a1 1 0 0 0-.039.316C3 16 3 21 3 21a1 1 0 0 0 1 1h16a1 1 0 0 0 1-1s0-5-.013-5M16 7.904c.259 0 .518-.095.707-.283a1 1 0 0 0 0-1.414L12 1.5L7.293 6.207a1 1 0 0 0 0 1.414c.189.189.448.283.707.283s.518-.094.707-.283L11 5.328V12a1 1 0 0 0 2 0V5.328l2.293 2.293a1 1 0 0 0 .707.283"/></svg></button>
            <input type="text" class="search-input">
        </div>
    </nav>
</template>

<script setup>

import { defineEmits } from 'vue';

const emit = defineEmits(["open"])
const handleAddImage = () => {
    emit('open')
};
</script>

<style scoped>
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    /* background-color: #333; */
    border-bottom: 2px solid gray;
    color: white;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.navbar-logo h1 {
    /* margin: 0; */
    /* font-size: 2rem; */
    color: white;
}

.navbar-links {
    display: flex;
    list-style: none;
    gap: 20px;
    margin: 0;
    padding: 0;
}

.navbar-links li a {
    text-decoration: none;
    color: white;
    font-size: 1rem;
    transition: color 0.3s;
}

.navbar-links li a:hover {
    color: lightgray;
}

.navbar-options{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
}

.navbar-button {
    padding: 10px 15px;
    border: none;
    border-radius: 8px;
    background-color: #61BE8B;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
}

.navbar-button svg{
    height: 25px;
    width: 25px;
}

.navbar-button:hover {
    background-color: #3b9e67;
    transform: translateY(-2px);
}

.navbar-button:active {
    transform: translateY(0);
}


.search-input{
    padding: 10px 20px;
    border-radius: 20px;
    background-color: #202322;
    border: 1px solid rgba(106, 106, 106, 0.186);
    outline: none;
    color: #fff;
}
</style>