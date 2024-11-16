<template>
  <div class="min-h-screen bg-white py-16 mt-16">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Contact Header -->
      <div class="text-center mb-12">
        <h1 class="text-4xl font-bold mb-4">Contact Us</h1>
        <p class="text-lg text-gray-600">
          Get in touch with us through any of these channels
        </p>
      </div>

      <!-- Contact Cards Grid -->
      <div class="max-w-3xl mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <!-- Phone -->
          <a
            href="tel:+18683881452"
            class="bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow duration-300"
          >
            <div class="flex items-center space-x-4">
              <div class="bg-blue-50 p-3 rounded-full">
                <span class="material-icons text-blue-600">phone</span>
              </div>
              <div>
                <h3 class="text-lg font-semibold mb-1">Phone</h3>
                <p class="text-gray-600">+1 (868) 388-1452</p>
              </div>
            </div>
          </a>

          <!-- WhatsApp -->
          <a
            href="https://wa.me/18683881452"
            target="_blank"
            class="bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow duration-300"
          >
            <div class="flex items-center space-x-4">
              <div class="bg-green-50 p-3 rounded-full">
                <span class="material-icons text-green-600">chat</span>
              </div>
              <div>
                <h3 class="text-lg font-semibold mb-1">WhatsApp</h3>
                <p class="text-gray-600">+1 (868) 388-1452</p>
              </div>
            </div>
          </a>

          <!-- Email -->
          <a
            href="mailto:Piarcoairportguesthouse@gmail.com"
            class="bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow duration-300"
          >
            <div class="flex items-center space-x-4">
              <div class="bg-red-50 p-3 rounded-full">
                <span class="material-icons text-red-600">email</span>
              </div>
              <div>
                <h3 class="text-lg font-semibold mb-1">Email</h3>
                <p class="text-gray-600">Piarcoairportguesthouse@gmail.com</p>
              </div>
            </div>
          </a>

          <!-- Location -->
          <div
            class="bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow duration-300"
          >
            <div class="flex items-center space-x-4">
              <div class="bg-purple-50 p-3 rounded-full">
                <span class="material-icons text-purple-600">location_on</span>
              </div>
              <div>
                <h3 class="text-lg font-semibold mb-1">Address</h3>
                <p class="text-gray-600">Piarco, Trinidad and Tobago</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Booking Links -->
        <div class="mt-12 grid grid-cols-1 md:grid-cols-2 gap-6">
          <a
            href="https://www.airbnb.com/"
            target="_blank"
            class="flex items-center justify-center space-x-2 bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow duration-300"
          >
            <span class="material-icons text-red-400">home</span>
            <span>Book on Airbnb</span>
          </a>
          <a
            href="https://www.booking.com/hotel/tt/piarco-airport-guest-house.en-gb.html?label=piarco-9mvhvzBnDhpUYy2fCFY69gS418821260587%3Apl%3Ata%3Ap15%3Ap2%3Aac%3Aap%3Aneg%3Afi%3Atikwd-119611731178%3Alp9075957%3Ali%3Adec%3Adm%3Appccp%3DUmFuZG9tSVYkc2RlIyh9YcsZ-Id2vkzI8vtHPrjul3A&sid=ec989a848689de66a6467bed310e5075&aid=375038&ucfs=1&arphpl=1&dest_id=-1360570&dest_type=city&group_adults=2&req_adults=2&no_rooms=1&group_children=0&req_children=0&hpos=1&hapos=1&sr_order=popularity&srpvid=b3906f6f4d9d0073&srepoch=1731772259&from=searchresults"
            target="_blank"
            class="flex items-center justify-center space-x-2 bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow duration-300"
          >
            <span class="material-icons text-blue-400">hotel</span>
            <span>Book on Booking.com</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
