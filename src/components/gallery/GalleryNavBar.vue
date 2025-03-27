<template>
    <nav class="navbar">
        <div class="navbar-logo">
            <h1>Dashboard</h1>
        </div>
        <ul class="navbar-links">
            <li>
                <router-link to="/">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"><path fill="#ffffff" d="M20 10a1 1 0 1 0-2 0zM6 10a1 1 0 0 0-2 0zm14.293 2.707a1 1 0 0 0 1.414-1.414zM12 3l.707-.707a1 1 0 0 0-1.414 0zm-9.707 8.293a1 1 0 1 0 1.414 1.414zM7 22h10v-2H7zm13-3v-9h-2v9zM6 19v-9H4v9zm15.707-7.707l-9-9l-1.414 1.414l9 9zm-10.414-9l-9 9l1.414 1.414l9-9zM17 22a3 3 0 0 0 3-3h-2a1 1 0 0 1-1 1zM7 20a1 1 0 0 1-1-1H4a3 3 0 0 0 3 3z"/></svg>
                </router-link>
            </li>
            <li>
                <router-link to="/favorites">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
                    <path fill="currentColor" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2c-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/>
                </svg>
                </router-link>
            </li>
        </ul>

        <div class="navbar-options">
            <button class="navbar-button" @click="handleAddImage"><svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24"><path fill="#ffffff" d="M20.987 16a1 1 0 0 0-.039-.316l-2-6A1 1 0 0 0 18 9h-4v2h3.279l1.667 5H5.054l1.667-5H10V9H6a1 1 0 0 0-.948.684l-2 6a1 1 0 0 0-.039.316C3 16 3 21 3 21a1 1 0 0 0 1 1h16a1 1 0 0 0 1-1s0-5-.013-5M16 7.904c.259 0 .518-.095.707-.283a1 1 0 0 0 0-1.414L12 1.5L7.293 6.207a1 1 0 0 0 0 1.414c.189.189.448.283.707.283s.518-.094.707-.283L11 5.328V12a1 1 0 0 0 2 0V5.328l2.293 2.293a1 1 0 0 0 .707.283"/></svg></button>
            <form @submit.prevent="submitSearch">
                <input 
                    v-model="searchQuery" 
                    class="search-input" 
                    type="text" 
                    placeholder="Buscar..."
                >
            </form>             
        </div>
    </nav>
</template>

<script setup>
import { defineEmits, defineProps, ref } from 'vue';

const searchQuery = ref('');

const props = defineProps({
    currentView: {
        type: String,
        default: 'all'
    }
});

const emit = defineEmits(['open', 'toggle-view', 'search']);

const handleAddImage = () => {
    emit('open');
};

const changeView = (view) => {
    emit('toggle-view', view);
};

const submitSearch = () => {
    // Emit the search event with the current search query
    emit('search', searchQuery.value);
    console.log('Searching for:', searchQuery.value);    
    searchQuery.value = '';
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
    justify-content: center;
    align-items:center;
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