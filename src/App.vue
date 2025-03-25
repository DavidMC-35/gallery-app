
<template>
  <div class="dashboard">
    <GalleryNav @open="isModalOpen = true"></GalleryNav>    
    <GalleryModal :isOpen="isModalOpen" >
      <GalleryForm @close="isModalOpen = false" @new-image="handleFormSubmit"></GalleryForm>
    </GalleryModal>
    <GalleryContainer></GalleryContainer>
  </div>
</template>

<script setup>
    
    import {ref} from "vue"

    import GalleryModal from "./components/gallery/GalleryModal.vue"
    import GalleryForm from './components/gallery/GalleryForm.vue'
    import GalleryNav from './components/gallery/GalleryNavBar.vue'
    import GalleryContainer from './components/gallery/GalleryContainer.vue'

    const gallery = ref([])
    const isModalOpen = ref(false)

    const handleFormSubmit = (data) => {
      console.log("Datos del formulario:", data)
      isModalOpen.value = false
    }
    
</script>

<style scoped>

  .dashboard{
    border: 1px solid red;
    height: 100vh;
    width: 100%;
  }

</style>
