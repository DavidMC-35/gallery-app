<template>
  <div class="dashboard">
    <div class="main-content">
      <GalleryNav 
        @open="isModalOpen = true"
        @search="searchQuery"
      ></GalleryNav>   
      
      <GalleryModal 
        :isOpen="isModalOpen" 
        @close="isModalOpen = false">
        <GalleryForm @new-image="handleFormSubmit"></GalleryForm>
      </GalleryModal>

      <router-view 
        :gallery="gallery"
        :favorites="galleryFavorites"
        @toggle-favorite="toggleFavorite"
      ></router-view>
    </div>
  </div>
</template>

<script setup>
    import { ref, computed, onMounted } from "vue"
    import { useRoute } from 'vue-router'
    import GalleryModal from "./components/gallery/GalleryModal.vue"
    import GalleryForm from './components/gallery/GalleryForm.vue'
    import GalleryNav from './components/gallery/GalleryNavBar.vue'

    // const route = useRoute()
    const gallery = ref([])
    const isModalOpen = ref(false)
    
    // const currentView = ref('all') // 'all' o 'favorites'
    // const currentRouteName = computed(() => route.name)

//     const handleViewChange = (view) => {
//     if (view === 'favorites') {
//       router.push('/favorites')
//     } else {
//       router.push('/')
//     }
// }

    // Función para cambiar entre vistas
    // const toggleView = (view) => {
    //   currentView.value = view;
    //   console.log('Vista cambiada a:', view);
    // }


    // Función para manejar la búsqueda
    const searchQuery = (query) => {
      console.log('Buscando:', query);
      const filteredImages = gallery.value.filter(img => img.description.toLowerCase().includes(query.toLowerCase()));
      console.log('Resultados de búsqueda:', filteredImages);
    }

    //Función para identificar las imágenes favoritas en el array gallery
    const galleryFavorites = computed(() => {
      return gallery.value.filter(image => image.favorite === true);
    });

    // Función para cambiar el estado de favorito de una imagen
    const toggleFavorite = (imageId) => {
      const imageIndex = gallery.value.findIndex(image => image.id === imageId);
      if (imageIndex !== -1) {
        gallery.value[imageIndex].favorite = !gallery.value[imageIndex].favorite;
        console.log('Imagen favorita cambiada:', imageId, 'Estado:', gallery.value[imageIndex].favorite);
        console.log('Total de favoritos:', galleryFavorites.value.length);
      }
    }
    
    // Implementación de la función fetchImages para cargar imágenes desde la API de Unsplash
    const fetchImages = async () => {
      try {
        const response = await fetch('https://api.unsplash.com/photos?client_id=jYg8SlU2GU3GNjmgg4FSXztqZqfpxcoTC4Ll2jzFBB4&per_page=18');
        const data = await response.json();
        console.log('Respuesta de la API:', data);

        gallery.value = data.map(item => ({
          id: item.id,
          date: new Date(item.created_at).toLocaleDateString(),
          file: item.urls.regular,
          description: item.alt_description || 'Sin descripción',
          author: item.user.name,
          profileImg: item.user.profile_image.large, 
          option: 'insertar',
          favorite: false,
        }));
        
        console.log('Imágenes cargadas:', gallery.value);
      } catch (error) {
        console.error('Error al cargar imágenes:', error);
      }
    }

    // Llama a la función fetchImages cuando se monta el componente
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
