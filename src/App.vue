
<template>
  <div class="dashboard">
    <GalleryNav @open="isModalOpen = true"></GalleryNav>   
    <GalleryModal :isOpen="isModalOpen" @close="isModalOpen = false">
      <GalleryForm @new-image="handleFormSubmit"></GalleryForm>
    </GalleryModal>
    <GalleryContainer :gallery="gallery" ></GalleryContainer>
  </div>
</template>

<script setup>
    
    import { ref, onMounted } from "vue" 

    import GalleryModal from "./components/gallery/GalleryModal.vue"
    import GalleryForm from './components/gallery/GalleryForm.vue'
    import GalleryNav from './components/gallery/GalleryNavBar.vue'
    import GalleryContainer from './components/gallery/GalleryContainer.vue'

    const gallery = ref([])
    const isModalOpen = ref(false)
    
    const fetchImages = async () => {
      try {
        const response = await fetch('https://api.unsplash.com/photos?client_id=jYg8SlU2GU3GNjmgg4FSXztqZqfpxcoTC4Ll2jzFBB4&per_page=18');
        const data = await response.json();
        
        gallery.value = data.map(item => ({
          id: item.id,
          date: new Date(item.created_at).toLocaleDateString(),
          file: item.urls.regular,
          description: item.alt_description || 'Sin descripción',
          author: item.user.name,
          option: 'insertar'
        }));
        
        console.log('Imágenes cargadas:', gallery.value);
      } catch (error) {
        console.error('Error al cargar imágenes:', error);
      }
    }

    onMounted(fetchImages);

    const handleFormSubmit = (data) => {
      gallery.value.push(data)
      console.log("Datos del formulario:", gallery.value)
      isModalOpen.value = false
    }
    
</script>

<style scoped>
  .dashboard{
    height: 100vh;
    width: 100%;
  }
</style>
