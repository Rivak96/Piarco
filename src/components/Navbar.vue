<template>
  <nav
    class="fixed w-full z-50 bg-white bg-opacity-90 backdrop-blur-sm shadow-sm"
  >
    <div class="max-w-7xl mx-auto px-4">
      <div class="flex justify-between items-center h-16">
        <!-- Logo/Brand -->
        <div class="flex items-center">
          <router-link to="/" class="text-xl font-bold text-blue-600">
            Piarco Guest House
          </router-link>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          <router-link
            v-for="item in navigationItems"
            :key="item.path"
            :to="item.path"
            class="text-gray-600 hover:text-blue-600 transition-colors duration-200"
          >
            {{ item.name }}
          </router-link>
        </div>

        <!-- Social Links -->
        <div class="hidden md:flex items-center space-x-4">
          <a
            v-for="social in socialLinks"
            :key="social.name"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-gray-600 hover:text-blue-600 transition-colors duration-200"
            :title="social.name"
          >
            <span class="material-icons">{{ social.icon }}</span>
          </a>
        </div>

        <!-- Mobile Menu Button -->
        <div class="md:hidden">
          <button
            @click="isOpen = !isOpen"
            class="text-gray-600 hover:text-blue-600 focus:outline-none"
          >
            <span class="material-icons">{{ isOpen ? "close" : "menu" }}</span>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div v-show="isOpen" class="md:hidden">
        <div class="px-2 pt-2 pb-3 space-y-1">
          <router-link
            v-for="item in navigationItems"
            :key="item.path"
            :to="item.path"
            class="block px-3 py-2 text-gray-600 hover:text-blue-600 transition-colors duration-200"
            @click="isOpen = false"
          >
            {{ item.name }}
          </router-link>

          <!-- Mobile Social Links -->
          <div class="flex space-x-4 px-3 py-2">
            <a
              v-for="social in socialLinks"
              :key="social.name"
              :href="social.url"
              target="_blank"
              rel="noopener noreferrer"
              class="text-gray-600 hover:text-blue-600 transition-colors duration-200"
            >
              <span class="material-icons">{{ social.icon }}</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

const isOpen = ref(false);

const navigationItems = [
  { name: "Home", path: "/" },
  { name: "Rooms", path: "/rooms" },
  { name: "Gallery", path: "/gallery" },
  { name: "Contact", path: "/contact" },
];

const socialLinks = [
  {
    name: "WhatsApp",
    url: "https://wa.me/18681234567", // Replace with actual WhatsApp number
    icon: "whatsapp",
  },
  {
    name: "Airbnb",
    url: "https://www.airbnb.com/s/homes?c=.pi0.pk988372260_125143042276&sem_automaid=true&gad_source=1&gclid=Cj0KCQiAouG5BhDBARIsAOc08RTNTQVpWWsMv7YG6BgjRKG-aPj00Ot9aYYEHAO831k0T9M1UZsg6CMaAuQXEALw_wcB&gclsrc=aw.ds&dynamic_product_ids%5B%5D=908820191854785508&omni_page_id=27964", // Replace with actual Airbnb listing URL
    icon: "house",
  },
  {
    name: "Booking.com",
    url: "https://www.booking.com/hotel/tt/piarco-airport-guest-house.en-gb.html?label=piarco-9mvhvzBnDhpUYy2fCFY69gS418821260587%3Apl%3Ata%3Ap15%3Ap2%3Aac%3Aap%3Aneg%3Afi%3Atikwd-119611731178%3Alp9075957%3Ali%3Adec%3Adm%3Appccp%3DUmFuZG9tSVYkc2RlIyh9YcsZ-Id2vkzI8vtHPrjul3A&sid=ec989a848689de66a6467bed310e5075&aid=375038&ucfs=1&arphpl=1&dest_id=-1360570&dest_type=city&group_adults=2&req_adults=2&no_rooms=1&group_children=0&req_children=0&hpos=1&hapos=1&sr_order=popularity&srpvid=b3906f6f4d9d0073&srepoch=1731772260&from=searchresults", // Replace with actual Booking.com listing URL
    icon: "book_online",
  },
];
</script>
