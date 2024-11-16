<template>
  <div class="min-h-screen bg-white py-16 mt-16">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Location Header -->
      <div class="text-center mb-12">
        <h1 class="text-4xl font-bold mb-4">Our Location</h1>
        <p class="text-lg text-gray-600">
          Conveniently located near Piarco International Airport with easy access to local attractions
        </p>
      </div>

      <!-- Map and Info Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-16">
        <!-- Main Map -->
        <div class="lg:col-span-2">
          <div class="bg-white rounded-xl shadow-lg overflow-hidden">
            <div id="map" class="h-[600px]"></div>
          </div>
        </div>

        <!-- Location Details -->
        <div class="space-y-6">
          <!-- Address Card -->
          <div class="bg-white rounded-xl shadow-lg p-6">
            <h3 class="text-xl font-semibold mb-4 flex items-center">
              <span class="material-icons text-blue-600 mr-2">location_on</span>
              Address
            </h3>
            <p class="text-gray-600">Piarco<br>Trinidad and Tobago</p>
            <button
              @click="copyAddress"
              class="mt-4 text-blue-600 hover:text-blue-700 text-sm flex items-center"
            >
              <span class="material-icons text-sm mr-1">content_copy</span>
              Copy Address
            </button>
          </div>

          <!-- Getting Here Card -->
          <div class="bg-white rounded-xl shadow-lg p-6">
            <h3 class="text-xl font-semibold mb-4">Getting Here</h3>
            <ul class="space-y-4">
              <li v-for="transport in transportOptions" :key="transport.text"
                  class="flex items-start">
                <span class="material-icons text-blue-600 mr-3">{{ transport.icon }}</span>
                <span class="text-gray-600">{{ transport.text }}</span>
              </li>
            </ul>
          </div>

          <!-- Contact Card -->
          <div class="bg-white rounded-xl shadow-lg p-6">
            <h3 class="text-xl font-semibold mb-4">Need Directions?</h3>
            <p class="text-gray-600 mb-4">
              Feel free to contact us for detailed directions or transportation arrangements.
            </p>
            <div class="space-y-3">
              <a 
                href="tel:+18681234567"
                class="flex items-center text-blue-600 hover:text-blue-700"
              >
                <span class="material-icons mr-2">phone</span>
                +1 (868) 123-4567
              </a>
              <a 
                href="https://wa.me/18681234567"
                target="_blank"
                class="flex items-center text-blue-600 hover:text-blue-700"
              >
                <span class="material-icons mr-2">whatsapp</span>
                WhatsApp Us
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- Nearby Attractions -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold mb-8 text-center">Nearby Attractions</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div 
            v-for="attraction in nearbyAttractions" 
            :key="attraction.name"
            class="bg-white rounded-xl shadow-lg p-6"
          >
            <span class="material-icons text-blue-600 text-3xl mb-4">{{ attraction.icon }}</span>
            <h3 class="text-lg font-semibold mb-2">{{ attraction.name }}</h3>
            <p class="text-gray-600 mb-2">{{ attraction.description }}</p>
            <p class="text-sm text-blue-600">{{ attraction.distance }}</p>
          </div>
        </div>
      </div>

      <!-- Local Transportation -->
      <div>
        <h2 class="text-3xl font-bold mb-8 text-center">Local Transportation</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div 
            v-for="transport in localTransportation" 
            :key="transport.name"
            class="bg-white rounded-xl shadow-lg p-6"
          >
            <div class="flex items-start">
              <span class="material-icons text-blue-600 mr-3">{{ transport.icon }}</span>
              <div>
                <h3 class="text-lg font-semibold mb-2">{{ transport.name }}</h3>
                <p class="text-gray-600">{{ transport.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import L from 'leaflet'

const transportOptions = [
  {
    icon: 'flight',
    text: '5 minutes from Piarco International Airport. Free pickup available for guests.'
  },
  {
    icon: 'local_parking',
    text: 'Free parking available on premises. Easy access from Churchill Roosevelt Highway.'
  },
  {
    icon: 'directions_bus',
    text: 'Public transportation available within 5 minutes walking distance.'
  },
  {
    icon: 'schedule',
    text: '25 minutes drive to Port of Spain, perfect for business travelers.'
  }
]

const nearbyAttractions = [
  {
    icon: 'flight',
    name: 'Airport',
    description: 'Piarco International Airport',
    distance: '5 min drive'
  },
  {
    icon: 'shopping_cart',
    name: 'Shopping',
    description: 'Local shops and convenience stores',
    distance: '5 min walk'
  },
  {
    icon: 'restaurant',
    name: 'Dining',
    description: 'Various local restaurants',
    distance: '5-10 min walk'
  },
  {
    icon: 'location_city',
    name: 'City Center',
    description: 'Port of Spain',
    distance: '25 min drive'
  }
]

const localTransportation = [
  {
    icon: 'local_taxi',
    name: 'Taxi Service',
    description: 'Reliable taxi services available 24/7. We can arrange pickup for you.'
  },
  {
    icon: 'directions_bus',
    name: 'Public Transport',
    description: 'Regular bus service to Port of Spain and other major areas.'
  },
  {
    icon: 'directions_car',
    name: 'Car Rental',
    description: 'Multiple car rental options available at the airport.'
  }
]

const copyAddress = () => {
  navigator.clipboard.writeText('Piarco, Trinidad and Tobago')
  // You could add a toast notification here
}

onMounted(() => {
  // Initialize map
  const map = L.map('map').setView([10.607168, -61.350764], 15)

  // Add OpenStreetMap tiles
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors',
    maxZoom: 19
  }).addTo(map)

  // Add marker for guest house location
  L.marker([10.607168, -61.350764])
    .addTo(map)
    .bindPopup('Piarco Guest House')
    .openPopup()

  // Add circle to show 5-minute walking radius
  L.circle([10.607168, -61.350764], {
    color: 'blue',
    fillColor: '#30a0ff',
    fillOpacity: 0.1,
    radius: 500 // 500 meters ~ 5-minute walk
  }).addTo(map)
})
</script>