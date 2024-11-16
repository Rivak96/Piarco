<template>
  <div class="min-h-screen bg-white py-16 mt-16">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Header -->
      <div class="text-center mb-12">
        <h1 class="text-4xl font-bold mb-4">Our Rooms</h1>
        <p class="text-lg text-gray-600">
          Comfortable and well-appointed rooms for your perfect stay
        </p>
      </div>

      <!-- Rooms Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div 
          v-for="room in rooms" 
          :key="room.title" 
          class="bg-white rounded-xl shadow-lg overflow-hidden"
        >
          <!-- Room Image -->
          <div class="aspect-w-16 aspect-h-9">
            <img 
              :src="room.image" 
              :alt="room.title"
              class="w-full h-full object-cover"
            >
          </div>

          <!-- Room Details -->
          <div class="p-6">
            <h2 class="text-2xl font-semibold mb-2">{{ room.title }}</h2>
            <p class="text-gray-600 mb-4">{{ room.description }}</p>

            <!-- Amenities -->
            <div class="grid grid-cols-2 gap-3 mb-6">
              <div 
                v-for="amenity in room.amenities" 
                :key="amenity.text"
                class="flex items-center space-x-2"
              >
                <span class="material-icons text-blue-600">{{ amenity.icon }}</span>
                <span>{{ amenity.text }}</span>
              </div>
            </div>

            <!-- Booking Links -->
            <div class="flex space-x-4">
              <a 
                :href="room.airbnbLink" 
                target="_blank"
                class="flex-1 flex items-center justify-center space-x-2 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors"
              >
                <span class="material-icons">home</span>
                <span>Book on Airbnb</span>
              </a>
              <a 
                :href="room.bookingLink" 
                target="_blank"
                class="flex-1 flex items-center justify-center space-x-2 bg-white border-2 border-blue-600 text-blue-600 px-4 py-2 rounded-lg hover:bg-blue-50 transition-colors"
              >
                <span class="material-icons">hotel</span>
                <span>Book on Booking.com</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const rooms = [
  {
    title: 'Mountain View Room',
    description: 'Spacious room with stunning views of the Northern Range mountains. Perfect for both leisure and business travelers.',
    image: '../assets/1.jpg',
    amenities: [
      { icon: 'ac_unit', text: 'Air Conditioning' },
      { icon: 'wifi', text: 'Free Wi-Fi' },
      { icon: 'tv', text: 'Smart TV' },
      { icon: 'king_bed', text: 'Queen Size Bed' },
      { icon: 'work', text: 'Work Desk' },
      { icon: 'bathroom', text: 'Private Bathroom' }
    ],
    airbnbLink: '#',
    bookingLink: '#'
  },
  {
    title: 'Deluxe Room',
    description: 'Comfortable room with modern amenities and a peaceful atmosphere. Ideal for short or extended stays.',
    image: '../assets/2.jpg',
    amenities: [
      { icon: 'ac_unit', text: 'Air Conditioning' },
      { icon: 'wifi', text: 'Free Wi-Fi' },
      { icon: 'tv', text: 'Smart TV' },
      { icon: 'single_bed', text: 'Double Bed' },
      { icon: 'work', text: 'Work Area' },
      { icon: 'bathroom', text: 'Private Bathroom' }
    ],
    airbnbLink: '#',
    bookingLink: '#'
  }
]
</script>