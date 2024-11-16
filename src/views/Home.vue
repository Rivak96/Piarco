<template>
  <div class="min-h-screen">
    <!-- Hero Section -->
    <HeroSlideshow />
    
    <!-- Property Highlights -->
    <section class="py-16 bg-gray-50">
      <div class="max-w-7xl mx-auto px-4">
        <!-- Section Header -->
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
            Property Highlights
          </h2>
          <p class="text-lg text-gray-600 max-w-2xl mx-auto">
            Experience comfort and convenience with our carefully curated amenities
          </p>
        </div>

        <!-- Highlights Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div 
            v-for="highlight in highlights" 
            :key="highlight.title"
            class="group"
          >
            <!-- Highlight Card -->
            <div class="relative bg-white rounded-xl shadow-sm hover:shadow-md transition-shadow duration-300 overflow-hidden">
              <!-- Semi-transparent background -->
              <div class="absolute inset-0 bg-blue-50 opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
              
              <!-- Content -->
              <div class="relative p-6">
                <!-- Icon -->
                <div class="mb-4 text-blue-600">
                  <span class="material-icons text-3xl">{{ highlight.icon }}</span>
                </div>
                
                <!-- Title -->
                <h3 class="text-xl font-semibold text-gray-900 mb-2">
                  {{ highlight.title }}
                </h3>
                
                <!-- Description -->
                <p class="text-gray-600">
                  {{ highlight.description }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Additional Features -->
        <div class="mt-16 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div 
            v-for="feature in additionalFeatures" 
            :key="feature.title"
            class="flex items-center space-x-3 bg-white p-4 rounded-lg shadow-sm"
          >
            <span class="material-icons text-blue-600">{{ feature.icon }}</span>
            <span class="text-gray-700">{{ feature.title }}</span>
          </div>
        </div>
      </div>
    </section>
    
    <!-- About Section -->
    <section class="py-16 bg-white">
      <div class="max-w-7xl mx-auto px-4">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <div>
            <h2 class="text-3xl font-bold mb-6">Experience Comfort & Convenience</h2>
            <p class="text-gray-600 mb-8">
              Located just minutes from Piarco International Airport, our guest house combines 
              modern amenities with Trinidad's warm hospitality. Whether you're here for business 
              or pleasure, our comfortable accommodations provide the perfect base for your stay.
            </p>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div 
                v-for="feature in quickFeatures" 
                :key="feature"
                class="flex items-center space-x-2"
              >
                <span class="material-icons text-green-500">check_circle</span>
                <span class="text-gray-700">{{ feature }}</span>
              </div>
            </div>
            
            <div class="mt-8">
              <router-link 
                to="/contact"
                class="inline-flex items-center space-x-2 bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition-colors duration-300"
              >
                <span>Contact Us</span>
                <span class="material-icons">arrow_forward</span>
              </router-link>
            </div>
          </div>
          
          <div class="grid grid-cols-2 gap-4">
            <div class="space-y-4">
              <img 
                src="../assets/1.jpg" 
                alt="Guest House Interior" 
                class="rounded-lg shadow-lg object-cover w-full h-48"
              >
              <img 
                src="../assets/2.jpg" 
                alt="Guest House Room" 
                class="rounded-lg shadow-lg object-cover w-full h-64"
              >
            </div>
            <div class="space-y-4 pt-8">
              <img 
                src="../assets/3.jpg" 
                alt="Guest House Amenities" 
                class="rounded-lg shadow-lg object-cover w-full h-64"
              >
              <img 
                src="../assets/4.jpg" 
                alt="Guest House View" 
                class="rounded-lg shadow-lg object-cover w-full h-48"
              >
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Location Preview -->
    <section class="bg-gray-50 py-16">
      <div class="max-w-7xl mx-auto px-4">
        <div class="text-center mb-12">
          <h2 class="text-3xl font-bold mb-4">Prime Location</h2>
          <p class="text-gray-600">
            Perfectly situated near Piarco International Airport and local attractions
          </p>
        </div>
        
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
          <div class="bg-white rounded-lg shadow-sm p-6">
            <h3 class="text-xl font-semibold mb-4">Getting Here</h3>
            <ul class="space-y-3">
              <li v-for="(detail, index) in locationDetails" 
                  :key="index"
                  class="flex items-center space-x-3"
              >
                <span class="material-icons text-blue-600">{{ detail.icon }}</span>
                <span class="text-gray-700">{{ detail.text }}</span>
              </li>
            </ul>
          </div>
          
          <div class="h-[400px] rounded-lg overflow-hidden shadow-sm">
            <div id="map" class="w-full h-full bg-gray-100"></div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import HeroSlideshow from '@/components/HeroSlideshow.vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

const highlights = [
  {
    icon: 'landscape',
    title: 'Mountain View',
    description: 'Enjoy breathtaking views of the Northern Range mountains from select rooms'
  },
  {
    icon: 'local_parking',
    title: 'Free Parking',
    description: 'Secure, on-site parking available for all guests at no additional cost'
  },
  {
    icon: 'computer',
    title: 'Workspace',
    description: 'Dedicated workspace with high-speed Wi-Fi perfect for remote work'
  },
  {
    icon: 'ac_unit',
    title: 'Air Conditioning',
    description: 'Climate-controlled rooms for your comfort in any weather'
  }
]

const additionalFeatures = [
  { icon: 'bathroom', title: 'Private Bathroom' },
  { icon: 'coffee', title: 'Coffee Maker' },
  { icon: 'wifi', title: 'Free Wi-Fi' },
  { icon: 'security', title: '24/7 Security' },
  { icon: 'water_drop', title: 'Hot Water' },
  { icon: 'kitchen', title: 'Full Kitchen' },
  { icon: 'tv', title: 'Smart TV' },
  { icon: 'restaurant', title: 'Dining Area' }
]

const quickFeatures = [
  'Free Airport Pickup',
  'Complimentary Breakfast',
  '24/7 Security',
  'Free Wi-Fi',
  'Air Conditioning',
  'Mountain Views',
  'Private Parking',
  'Work Space'
]

const locationDetails = [
  {
    icon: 'location_on',
    text: 'Located in Piarco, Trinidad and Tobago'
  },
  {
    icon: 'local_parking',
    text: 'Free parking available on premises'
  },
  {
    icon: 'schedule',
    text: '5 minutes from local restaurants and shops'
  },
  {
    icon: 'flight',
    text: '5 minutes from Piarco International Airport'
  }
]

onMounted(() => {
  // Initialize map
  const map = L.map('map').setView([10.607161, -61.350748], 15)
  
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(map)
  
  L.marker([10.607161, -61.350748])
    .addTo(map)
    .bindPopup('Piarco Guest House')
    .openPopup()
})
</script>

<style>
@import url('https://fonts.googleapis.com/icon?family=Material+Icons');
</style>