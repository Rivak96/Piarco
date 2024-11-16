<template>
  <div class="relative h-[90vh] overflow-hidden">
    <!-- Slideshow -->
    <div class="relative h-full">
      <transition-group name="slide" tag="div" class="h-full">
        <div
          v-for="(slide, index) in slides"
          :key="slide.id"
          v-show="currentSlide === index"
          class="absolute inset-0 w-full h-full"
        >
          <!-- Image with Ken Burns effect -->
          <div class="absolute inset-0 w-full h-full">
            <img
              :src="slide.image"
              :alt="slide.title"
              class="w-full h-full object-cover transform scale-105 animate-kenburns"
            />
          </div>

          <!-- Gradient Overlay -->
          <div
            class="absolute inset-0 bg-gradient-to-b from-black/50 via-black/40 to-black/60"
          >
            <!-- Text Content -->
            <div
              class="h-full flex flex-col items-center justify-center text-white px-4 md:px-8"
            >
              <!-- Title with animated underline -->
              <h1
                class="text-4xl md:text-6xl font-bold mb-4 text-center relative slide-up opacity-0"
                :style="`animation-delay: ${0}ms`"
              >
                {{ slide.title }}
                <span
                  class="block w-24 h-1 bg-white mx-auto mt-4 slide-line"
                ></span>
              </h1>

              <!-- Description -->
              <p
                class="text-xl md:text-2xl mb-8 text-center max-w-3xl slide-up opacity-0"
                :style="`animation-delay: ${200}ms`"
              >
                {{ slide.description }}
              </p>

              <!-- Feature Highlight -->
              <div
                class="bg-white/10 backdrop-blur-sm px-8 py-4 rounded-lg mb-12 transform slide-up opacity-0"
                :style="`animation-delay: ${400}ms`"
              >
                <p class="text-lg md:text-xl font-semibold flex items-center">
                  <span class="material-icons mr-3">{{ slide.icon }}</span>
                  {{ slide.highlight }}
                </p>
              </div>

              <!-- Booking Buttons -->
              <div
                class="flex flex-col sm:flex-row gap-4 sm:space-x-6 slide-up opacity-0"
                :style="`animation-delay: ${600}ms`"
              >
                <a
                  href="https://www.airbnb.com/rooms/908820191854785508?adults=1&children=0&infants=0&search_mode=regular_search&check_in=2024-11-17&check_out=2024-11-22&source_impression_id=p3_1731772695_P3atr3ppQIXa3efR&previous_page_section_name=1000&federated_search_id=c8a572cb-b399-4c6d-bb16-a9931d71ae9f"
                  target="_blank"
                  class="group bg-white text-gray-900 px-8 py-3 rounded-lg hover:bg-gray-100 transition-all duration-300 transform hover:scale-105"
                >
                  <span class="flex items-center justify-center">
                    <span class="material-icons mr-2 group-hover:text-red-500"
                      >home</span
                    >
                    Book on Airbnb
                  </span>
                </a>
                <a
                  href="https://www.booking.com/hotel/tt/piarco-airport-guest-house.en-gb.html?label=piarco-9mvhvzBnDhpUYy2fCFY69gS418821260587%3Apl%3Ata%3Ap15%3Ap2%3Aac%3Aap%3Aneg%3Afi%3Atikwd-119611731178%3Alp9075957%3Ali%3Adec%3Adm%3Appccp%3DUmFuZG9tSVYkc2RlIyh9YcsZ-Id2vkzI8vtHPrjul3A&sid=ec989a848689de66a6467bed310e5075&aid=375038&ucfs=1&arphpl=1&dest_id=-1360570&dest_type=city&group_adults=2&req_adults=2&no_rooms=1&group_children=0&req_children=0&hpos=1&hapos=1&sr_order=popularity&srpvid=b3906f6f4d9d0073&srepoch=1731772259&from=searchresults"
                  target="_blank"
                  class="group bg-blue-600 text-white px-8 py-3 rounded-lg hover:bg-blue-700 transition-all duration-300 transform hover:scale-105"
                >
                  <span class="flex items-center justify-center">
                    <span class="material-icons mr-2 group-hover:text-white"
                      >hotel</span
                    >
                    Book on Booking.com
                  </span>
                </a>
              </div>
            </div>
          </div>
        </div>
      </transition-group>
    </div>

    <!-- Navigation Dots -->
    <div
      class="absolute bottom-8 left-1/2 transform -translate-x-1/2 flex space-x-3 z-20"
    >
      <button
        v-for="(slide, index) in slides"
        :key="slide.id"
        @click="goToSlide(index)"
        class="w-3 h-3 rounded-full transition-all duration-500 relative"
        :class="
          currentSlide === index
            ? 'bg-white scale-125'
            : 'bg-white/50 hover:bg-white/75'
        "
      >
        <span class="sr-only">Slide {{ index + 1 }}</span>
        <!-- Progress indicator -->
        <svg
          v-if="currentSlide === index"
          class="absolute inset-0 w-full h-full -rotate-90"
          viewBox="0 0 100 100"
        >
          <circle
            class="progress-ring"
            cx="50"
            cy="50"
            r="45"
            fill="none"
            stroke="white"
            stroke-width="10"
          />
        </svg>
      </button>
    </div>

    <!-- Arrow Navigation -->
    <button
      @click="previousSlide"
      class="absolute left-4 top-1/2 transform -translate-y-1/2 text-white opacity-50 hover:opacity-100 transition-opacity duration-300 z-20"
    >
      <span class="material-icons text-5xl">chevron_left</span>
      <span class="sr-only">Previous slide</span>
    </button>
    <button
      @click="nextSlide"
      class="absolute right-4 top-1/2 transform -translate-y-1/2 text-white opacity-50 hover:opacity-100 transition-opacity duration-300 z-20"
    >
      <span class="material-icons text-5xl">chevron_right</span>
      <span class="sr-only">Next slide</span>
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const currentSlide = ref(0);
const slides = [
  {
    id: 1,
    image: "/images/1.jpg",
    title: "Welcome to Piarco Guest House",
    description:
      "Relaxed Accommodation Minutes from Piarco International Airport",
    highlight: "Your Perfect Transit Stay",
    icon: "flight",
  },
  {
    id: 2,
    image: "/images/2.jpg",
    title: "Modern Comfort",
    description: "Experience comfort and convenience",
    highlight: "Free Airport Pickup Available",
    icon: "local_taxi",
  },
  {
    id: 3,
    image: "/images/3.jpg",
    title: "Work & Relax",
    description: "Perfect for business and leisure",
    highlight: "Dedicated Workspace with Wi-Fi",
    icon: "computer",
  },
  {
    id: 4,
    image: "/images/4.jpg",
    title: "Contemporary Living",
    description: "Modern amenities for your comfort",
    highlight: "Air Conditioned Rooms",
    icon: "ac_unit",
  },
  {
    id: 5,
    image: "/images/5.jpg",
    title: "Your Home Away",
    description: "Comfortable spaces for relaxation",
    highlight: "Fully Equipped Kitchen",
    icon: "kitchen",
  },
  {
    id: 6,
    image: "/images/6.jpg",
    title: "Prime Location",
    description: "Minutes from major attractions",
    highlight: "5 Minutes from Airport",
    icon: "location_on",
  },
];

const goToSlide = (index) => {
  currentSlide.value = index;
  resetSlideshow();
};

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length;
  resetSlideshow();
};

const previousSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length;
  resetSlideshow();
};

let intervalId = null;
const slideDuration = 6000; // 6 seconds per slide

const startSlideshow = () => {
  intervalId = setInterval(nextSlide, slideDuration);
};

const stopSlideshow = () => {
  if (intervalId) clearInterval(intervalId);
};

const resetSlideshow = () => {
  stopSlideshow();
  startSlideshow();
};

onMounted(() => {
  startSlideshow();
});

onBeforeUnmount(() => {
  stopSlideshow();
});
</script>

<style scoped>
/* Slide Transitions */
.slide-enter-active,
.slide-leave-active {
  transition: all 1s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: scale(1.1);
}

.slide-leave-to {
  opacity: 0;
  transform: scale(0.9);
}

/* Ken Burns Effect */
@keyframes kenburns {
  0% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}

.animate-kenburns {
  animation: kenburns 20s ease-out both;
}

/* Slide Up Animation */
@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.slide-up {
  animation: slideUp 1s ease-out forwards;
}

/* Progress Ring Animation */
@keyframes progress {
  from {
    stroke-dashoffset: 283;
  }
  to {
    stroke-dashoffset: 0;
  }
}

.progress-ring {
  stroke-dasharray: 283;
  stroke-dashoffset: 283;
  animation: progress 6s linear forwards;
}

/* Underline Animation */
@keyframes slideRight {
  from {
    width: 0;
  }
  to {
    width: 6rem;
  }
}

.slide-line {
  animation: slideRight 1s ease-out forwards;
}
</style>
