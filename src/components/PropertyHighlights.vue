<template>
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
      <div class="mt-16 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
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
</template>

<script setup>
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
    icon: 'laptop',
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
  { icon: 'bathtub', title: 'Private Bathroom' },
  { icon: 'coffee', title: 'Coffee Maker' },
  { icon: 'wifi', title: 'Free Wi-Fi' },
  { icon: 'security', title: '24/7 Security' },
  { icon: 'water_drop', title: 'Hot Water' },
  { icon: 'kitchen', title: 'Full Kitchen' },
  { icon: 'tv', title: 'Smart TV' },
  { icon: 'restaurant', title: 'Dining Area' }
]
</script>