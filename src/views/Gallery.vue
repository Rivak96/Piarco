<template>
  <div class="min-h-screen bg-white py-16 mt-16">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Gallery Header -->
      <div class="text-center mb-12">
        <h1 class="text-4xl font-bold mb-4">Our Gallery</h1>
        <p class="text-lg text-gray-600">Take a tour of our comfortable accommodations and facilities</p>
      </div>

      <!-- Gallery Categories -->
      <div class="flex flex-wrap justify-center gap-4 mb-8">
        <button 
          v-for="category in categories" 
          :key="category"
          @click="selectedCategory = category"
          class="px-4 py-2 rounded-full transition-colors duration-300"
          :class="selectedCategory === category 
            ? 'bg-blue-600 text-white' 
            : 'bg-gray-100 text-gray-700 hover:bg-gray-200'"
        >
          <span class="material-icons align-middle mr-1 text-sm">
            {{ getCategoryIcon(category) }}
          </span>
          {{ category }}
        </button>
      </div>

      <!-- Gallery Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div 
          v-for="image in filteredImages" 
          :key="image.id"
          class="group cursor-pointer relative"
          @click="openLightbox(image)"
        >
          <!-- Image -->
          <div class="aspect-w-4 aspect-h-3 rounded-lg overflow-hidden">
            <img 
              :src="image.src" 
              :alt="image.title"
              class="w-full h-full object-cover transform transition-transform duration-300 group-hover:scale-105"
            >
          </div>
          
          <!-- Overlay -->
          <div class="absolute inset-0 bg-black bg-opacity-0 group-hover:bg-opacity-40 transition-opacity duration-300 rounded-lg">
            <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300">
              <div class="text-white text-center">
                <h3 class="text-lg font-semibold mb-1">{{ image.title }}</h3>
                <p class="text-sm">{{ image.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Lightbox -->
      <div 
        v-if="selectedImage"
        class="fixed inset-0 bg-black bg-opacity-90 z-50 flex items-center justify-center"
        @click="selectedImage = null"
      >
        <div class="relative max-w-4xl mx-4">
          <!-- Close Button -->
          <button 
            @click="selectedImage = null"
            class="absolute -top-12 right-0 text-white hover:text-gray-300"
          >
            <span class="material-icons">close</span>
          </button>

          <!-- Image -->
          <img 
            :src="selectedImage.src" 
            :alt="selectedImage.title"
            class="max-h-[80vh] w-auto"
          >

          <!-- Caption -->
          <div class="text-white text-center mt-4">
            <h3 class="text-xl font-semibold mb-2">{{ selectedImage.title }}</h3>
            <p class="text-gray-300">{{ selectedImage.description }}</p>
          </div>

          <!-- Navigation Buttons -->
          <button 
            v-if="currentImageIndex > 0"
            @click.stop="showPreviousImage"
            class="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-16 text-white hover:text-gray-300"
          >
            <span class="material-icons text-4xl">chevron_left</span>
          </button>
          <button 
            v-if="currentImageIndex < filteredImages.length - 1"
            @click.stop="showNextImage"
            class="absolute right-0 top-1/2 -translate-y-1/2 translate-x-16 text-white hover:text-gray-300"
          >
            <span class="material-icons text-4xl">chevron_right</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const selectedCategory = ref('All')
const selectedImage = ref(null)

const categories = ['All', 'Rooms', 'Facilities', 'Exterior', 'Views']

const getCategoryIcon = (category) => {
  const icons = {
    'All': 'grid_view',
    'Rooms': 'bed',
    'Facilities': 'local_cafe',
    'Exterior': 'home',
    'Views': 'landscape'
  }
  return icons[category]
}

const images = [
  {
    id: 1,
    src: '../assets/1.jpg',
    title: 'Modern Bedroom',
    description: 'Spacious bedroom with mountain view',
    category: 'Rooms'
  },
  {
    id: 2,
    src: '../assets/2.jpg',
    title: 'Cozy Living Area',
    description: 'Comfortable seating area with natural light',
    category: 'Rooms'
  },
  {
    id: 3,
    src: '../assets/3.jpg',
    title: 'Fully Equipped Kitchen',
    description: 'Modern kitchen with all necessary amenities',
    category: 'Facilities'
  },
  {
    id: 4,
    src: '../assets/4.jpg',
    title: 'Modern Bathroom',
    description: 'Clean and modern bathroom facilities',
    category: 'Facilities'
  },
  {
    id: 5,
    src: '../assets/5.jpg',
    title: 'Guest House Exterior',
    description: 'Beautiful exterior view of the property',
    category: 'Exterior'
  },
  {
    id: 6,
    src: '../assets/6.jpg',
    title: 'Mountain View',
    description: 'Breathtaking view of the Northern Range',
    category: 'Views'
  }
]

const filteredImages = computed(() => {
  if (selectedCategory.value === 'All') return images
  return images.filter(image => image.category === selectedCategory.value)
})

const currentImageIndex = computed(() => {
  if (!selectedImage.value) return -1
  return filteredImages.value.findIndex(img => img.id === selectedImage.value.id)
})

const openLightbox = (image) => {
  selectedImage.value = image
}

const showPreviousImage = () => {
  const newIndex = currentImageIndex.value - 1
  if (newIndex >= 0) {
    selectedImage.value = filteredImages.value[newIndex]
  }
}

const showNextImage = () => {
  const newIndex = currentImageIndex.value + 1
  if (newIndex < filteredImages.value.length) {
    selectedImage.value = filteredImages.value[newIndex]
  }
}
</script>