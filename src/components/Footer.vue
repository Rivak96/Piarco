<template>
  <footer class="bg-gray-900 text-gray-300">
    <!-- Main Footer Content -->
    <div class="max-w-7xl mx-auto px-4 py-12">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        <!-- About Section -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">
            Piarco Guest House
          </h3>
          <p class="mb-4">
            Your perfect stay near Piarco International Airport with mountain
            views and modern amenities.
          </p>
          <div class="flex space-x-4">
            <a
              v-for="social in socials"
              :key="social.name"
              :href="social.url"
              target="_blank"
              rel="noopener noreferrer"
              class="text-gray-400 hover:text-white transition-colors duration-300"
            >
              <span class="material-icons">{{ social.icon }}</span>
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">Quick Links</h3>
          <ul class="space-y-2">
            <li v-for="link in quickLinks" :key="link.text">
              <router-link
                :to="link.to"
                class="hover:text-white transition-colors duration-300"
              >
                {{ link.text }}
              </router-link>
            </li>
          </ul>
        </div>

        <!-- Contact Info -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">Contact Us</h3>
          <ul class="space-y-3">
            <li v-for="contact in contactInfo" :key="contact.text">
              <a
                v-if="contact.link"
                :href="contact.link"
                class="flex items-center space-x-2 text-gray-300 hover:text-white transition-colors duration-300"
              >
                <span class="material-icons">{{ contact.icon }}</span>
                <span>{{ contact.text }}</span>
              </a>
              <div v-else class="flex items-center space-x-2">
                <span class="material-icons">{{ contact.icon }}</span>
                <span>{{ contact.text }}</span>
              </div>
            </li>
          </ul>
        </div>
        <!-- Book Now -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">Book Your Stay</h3>
          <div class="space-y-4">
            <a
              v-for="booking in bookingLinks"
              :key="booking.name"
              :href="booking.url"
              target="_blank"
              rel="noopener noreferrer"
              class="flex items-center space-x-2 text-gray-300 hover:text-white transition-colors duration-300"
            >
              <span class="material-icons">{{ booking.icon }}</span>
              <span>Book on {{ booking.name }}</span>
            </a>
          </div>
        </div>
      </div>
    </div>

    <!-- Bottom Bar -->
    <div class="border-t border-gray-800">
      <div class="max-w-7xl mx-auto px-4 py-6">
        <div class="flex flex-col md:flex-row justify-between items-center">
          <p class="text-sm">
            © {{ new Date().getFullYear() }} Piarco Guest House. All rights
            reserved.
          </p>
          <div class="flex space-x-4 mt-4 md:mt-0">
            <router-link
              v-for="link in bottomLinks"
              :key="link.text"
              :to="link.to"
              class="text-sm hover:text-white transition-colors duration-300"
            >
              {{ link.text }}
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const socials = [
  { name: "Facebook", icon: "facebook", url: "#" },
  { name: "Instagram", icon: "photo_camera", url: "#" },
  { name: "WhatsApp", icon: "chat", url: "https://wa.me/18681234567" },
];

const quickLinks = [
  { text: "Home", to: "/" },
  { text: "Rooms", to: "/rooms" },
  { text: "Gallery", to: "/gallery" },
  { text: "Contact", to: "/contact" },
];

const contactInfo = [
  { icon: "location_on", text: "Piarco, Trinidad and Tobago" },
  { icon: "phone", text: "+1 (868) 123-4567" },
  { icon: "email", text: "info@piarcoguesthouse.com" },
];

const bookingLinks = [
  { name: "Airbnb", icon: "home", url: "#" },
  { name: "Booking.com", icon: "hotel", url: "#" },
];

const bottomLinks = [
  { text: "Privacy Policy", to: "/privacy" },
  { text: "Terms of Service", to: "/terms" },
  { text: "About Host", to: "/about" },
];
</script>
