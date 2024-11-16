<template>
  <section class="py-16 bg-white">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Section Header -->
      <div class="text-center mb-12">
        <div class="flex items-center justify-center space-x-1 mb-4">
          <Star v-for="_ in 5" :key="_" class="w-6 h-6 text-yellow-400 fill-current" />
        </div>
        <h2 class="text-3xl font-bold mb-2">Guest Reviews</h2>
        <p class="text-xl text-gray-600">4.85 out of 5 stars from our amazing guests</p>
      </div>

      <!-- Reviews Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="review in reviews" 
          :key="review.id"
          class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow duration-300"
        >
          <!-- Review Header -->
          <div class="flex items-center mb-4">
            <div class="w-12 h-12 rounded-full overflow-hidden bg-gray-200 mr-4">
              <img 
                :src="`/api/placeholder/${review.id}/48`" 
                :alt="review.name"
                class="w-full h-full object-cover"
              />
            </div>
            <div>
              <h3 class="font-semibold text-gray-900">{{ review.name }}</h3>
              <p class="text-sm text-gray-500">{{ review.date }}</p>
            </div>
          </div>

          <!-- Star Rating -->
          <div class="flex space-x-1 mb-3">
            <Star 
              v-for="star in 5" 
              :key="star"
              :class="[
                'w-4 h-4',
                star <= review.rating ? 'text-yellow-400 fill-current' : 'text-gray-300'
              ]"
            />
          </div>

          <!-- Review Text -->
          <p class="text-gray-600 mb-4">{{ review.text }}</p>

          <!-- Source -->
          <div class="flex items-center text-sm text-gray-500">
            <component :is="review.source.icon" class="w-4 h-4 mr-1" />
            <span>Posted on {{ review.source.name }}</span>
          </div>
        </div>
      </div>

      <!-- Review Stats -->
      <div class="mt-16 grid grid-cols-2 md:grid-cols-4 gap-8">
        <div 
          v-for="stat in reviewStats" 
          :key="stat.label"
          class="text-center"
        >
          <div class="text-3xl font-bold text-blue-600 mb-2">{{ stat.value }}</div>
          <div class="text-gray-600">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Star, Airplay, BookOpen } from 'lucide-react'

const reviews = [
  {
    id: 1,
    name: 'Sarah M.',
    date: 'March 2024',
    rating: 5,
    text: 'Amazing location near the airport! The mountain views were breathtaking and the hosts were incredibly welcoming. Perfect for both short and long stays.',
    source: {
      name: 'Airbnb',
      icon: Airplay
    }
  },
  {
    id: 2,
    name: 'James R.',
    date: 'February 2024',
    rating: 5,
    text: 'Excellent accommodation with all the amenities you need. The workspace was perfect for my business trip, and the airport proximity was a huge plus.',
    source: {
      name: 'Booking.com',
      icon: BookOpen
    }
  },
  {
    id: 3,
    name: 'Maria L.',
    date: 'January 2024',
    rating: 5,
    text: 'Clean, comfortable, and convenient! The free airport pickup made our late arrival so much easier. The full kitchen was a great bonus.',
    source: {
      name: 'Airbnb',
      icon: Airplay
    }
  }
]

const reviewStats = [
  { value: '4.85', label: 'Average Rating' },
  { value: '500+', label: 'Happy Guests' },
  { value: '98%', label: 'Would Recommend' },
  { value: '100%', label: 'Clean & Comfort' }
]
</script>