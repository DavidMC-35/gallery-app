<template>
    <div class="gallery-image">
        <img src="https://images.unsplash.com/photo-1742226111230-1f7620e64851?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" alt="">
        <div class="info">
            <p>Hola</p>
        </div>
    </div>
</template>
<script setup></script>

<style scoped>

    .gallery-image{
        height: 400px;
        width: 300px;
        background-color: lightgray;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        border-radius: 12px;
    }

    .gallery-image img{
        height: 250px;
        width: 250px;
    }

</style>