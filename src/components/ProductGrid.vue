<template>
  <section class="py-12 relative bg-gray-50 after:pointer-events-none after:absolute after:inset-x-0 after:bottom-0 after:h-px after:bg-gray-200">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <h2 class="text-2xl font-bold text-gray-900 mb-6">Products</h2>
      <!-- Filters -->
      <div class="mb-6 flex flex-wrap items-center gap-4">
        <Listbox as="div" v-model="selectedCategory">
          <div class="select-wrapper relative">
            <ListboxButton class="flex-1 w-full border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm">
              <span class="col-start-1 row-start-1 flex items-center gap-3 pr-6">
                <span class="block truncate capitalize">{{ selectedCategory }}</span>
              </span>
              <ChevronDownIcon class="icon col-start-1 row-start-1 size-5 self-center justify-self-end text-gray-900 absolute sm:size-4" aria-hidden="true" />
            </ListboxButton>
            <transition leave-active-class="transition ease-in duration-100" leave-from-class="" leave-to-class="opacity-0">
              <ListboxOptions class="absolute z-10 mt-1 max-h-56 w-full overflow-auto border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm sm:text-sm">
                <ListboxOption as="template" :value="'All Categories'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">All Categories</span>
                    </div>
                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'audio'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Audio</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'computers'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Computers</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'gadgets'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Gadgets</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
              </ListboxOptions>
            </transition>
          </div>
        </Listbox>
        <Listbox as="div" v-model="sortBy">
          <div class="select-wrapper relative">
            <ListboxButton class="flex-1 w-full border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm">
              <span class="col-start-1 row-start-1 flex items-center gap-3 pr-6">
                <span class="block truncate capitalize">{{ sortBy }}</span>
              </span>
              <ChevronDownIcon class="icon col-start-1 row-start-1 size-5 self-center justify-self-end text-gray-900 absolute sm:size-4" aria-hidden="true" />
            </ListboxButton>
            <transition leave-active-class="transition ease-in duration-100" leave-from-class="" leave-to-class="opacity-0">
              <ListboxOptions class="absolute z-10 mt-1 max-h-56 w-full overflow-auto border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm sm:text-sm">
                <ListboxOption as="template" :value="'Sort By'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Sort By</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Price: High to Low'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Price: High to Low</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Price: Low to High'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Price: Low to High</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Name: A-Z'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Name: A-Z</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-600', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Name: Z-A'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-gray-600', 'rounded-xl relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'block truncate']">Name: Z-A</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-2']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
              </ListboxOptions>
            </transition>
          </div>
        </Listbox>
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search products..."
          class="flex-1 border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm"
        />
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
            v-for="product in paginatedProducts"
            :key="product.id"
            class="flex flex-col flex-grow rounded-2xl bg-white shadow-sm p-6 ring-1 ring-gray-200"
        >
          <img
              :src="product.image"
              :alt="product.name"
              class="w-full h-56 object-contain"
          />
          <div class="flex flex-col flex-grow pt-4">
            <h3 class="text-lg font-semibold text-gray-900">{{ product.name }}</h3>
            <p class="flex-grow mt-2 text-gray-600 text-sm">{{ product.description }}</p>
            <div class="mt-4 flex flex-col">
              <span class="text-gray-900 font-bold mb-2">${{ product.price }}</span>
              <button
                  class="bg-gray-900 text-white px-7 py-2 rounded-md hover:bg-gray-700 transition"
              >
                Add to Cart
              </button>
            </div>
          </div>
        </div>
      </div>
      <Pagination :totalPages="totalPages"
                  :totalProducts="totalProducts"
                  :perPage="perPage"
                  :currentPage="currentPage"
                  @pageChanged="changePage" />
    </div>
  </section>
</template>

<script>
import { Listbox, ListboxButton, ListboxLabel, ListboxOption, ListboxOptions } from '@headlessui/vue';
import { ChevronDownIcon } from '@heroicons/vue/20/solid';
import { CheckIcon } from '@heroicons/vue/20/solid';
import { reactive, ref, computed, watch } from 'vue';
import Pagination from "./Pagination.vue";

export default {
  name: "ProductGrid",
  components: {Listbox, ListboxButton, ListboxLabel, ListboxOption, ListboxOptions, Pagination, ChevronDownIcon, CheckIcon},
  setup(){
    const products = reactive([
      {
        id: 1,
        name: 'ASUS ROG Cetra True Wireless Earbuds',
        description: 'Low-latency TWS for gaming with ANC and dual-mode connectivity',
        price: 139.99,
        image: '../public/ASUSROGCetraTrueWirelessEarbuds.jpg'
      },
      {
        id: 2,
        name: 'Logitech G Pro X Superlight Wireless Mouse',
        description: 'Ultra-light wireless esports mouse with HERO 25K sensor',
        price: 149.99,
        image: '../public/LogitechGProXSuperlight.jpg'
      },
      {
        id: 3,
        name: 'Razer DeathAdder V4 Pro',
        description: 'High-precision wireless mouse with 45K DPI and optical switches',
        price: 169.99,
        image: '../public/DeathAdder.webp'
      },
      {
        id: 4,
        name: 'ASUS ROG Cetra SpeedNova (White)',
        description: 'TWS earbuds with 2.4GHz/BT dual wireless and adaptive ANC',
        price: 179.99,
        image: '../public/ASUSROGCetraSpeedNova.jpg'
      },
      {
        id: 5,
        name: 'SteelSeries Arctis Pro Wireless',
        description: 'Premium dual-wireless gaming headset with base station',
        price: 249.99,
        image: '../public/SteelSeriesArctisPro.webp'
      },
      {
        id: 6,
        name: 'Razer BlackShark V3 Pro',
        description: 'Wireless esports headset with clear mic and long battery life',
        price: 199.99,
        image: '../public/RazerBlackSharkV3Pro.png'
      },
      {
        id: 7,
        name: 'Logitech G733 LIGHTSPEED',
        description: 'Lightweight wireless headset with surround sound',
        price: 159.99,
        image: '../public/LogitechG733.webp'
      },
      {
        id: 8,
        name: 'Meta Quest 2 (64GB)',
        description: 'Standalone VR headset with up to 120Hz display support',
        price: 299.00,
        image: '../public/MetaQuest2.jpg'
      },
      {
        id: 9,
        name: 'MSI Claw A8 Handheld',
        description: '8-inch 120Hz Windows handheld for AAA gaming on the go',
        price: 799.99,
        image: '../public/MSIClawA8Handheld.png'
      },
      {
        id: 10,
        name: 'Razer Basilisk Mobile',
        description: 'Lightweight wireless mouse made for portability',
        price: 89.99,
        image: '../public/RazerBasilisk.webp'
      },
      {
        id: 11,
        name: 'Xbox Elite Wireless Controller Series 2',
        description: 'Pro-grade Xbox/PC controller with adjustable triggers and paddles',
        price: 179.99,
        image: '../public/XboxElite.webp'
      },
      {
        id: 12,
        name: 'Sony DualSense Wireless Controller (PS5)',
        description: 'Haptic feedback and adaptive triggers for immersive gameplay',
        price: 69.99,
        image: '../public/DualSenseWirelessController.jpg'
      },
      {
        id: 13,
        name: 'HyperX QuadCast S USB Microphone',
        description: 'RGB condenser mic with built-in pop filter for streaming',
        price: 129.99,
        image: '../public/HyperXQuadCastS.webp'
      },
      {
        id: 14,
        name: 'Secretlab TITAN Evo 2022 Gaming Chair',
        description: 'Ergonomic gaming chair with adjustable lumbar support',
        price: 549.00,
        image: '../public/SecretlabTitanevo2022.webp'
      },
      {
        id: 15,
        name: 'Keychron K6 Pro Mechanical Keyboard',
        description: 'Hot-swappable 65% wireless mechanical keyboard with RGB',
        price: 89.00,
        image: '../public/KeychronK6Pro.webp'
      }
    ]);
    const currentPage = ref(1);
    const perPage = ref(8);
    const selectedCategory = ref('All Categories');
    const sortBy = ref('Sort By');
    const searchQuery = ref('');

    const filteredAndSortedProducts = computed(() => {
      let filtered = products;

      if (selectedCategory.value && selectedCategory.value !== 'All Categories') {
        const categoryMap = {
          audio: ['Wireless Headphones', 'Bluetooth Speaker', 'Noise Cancelling Earbuds'],
          computers: ['Gaming Mouse', 'Mechanical Keyboard', 'Laptop Stand', 'HD Webcam', 'External SSD', 'Wireless Charger', 'Action Camera', 'Fitness Tracker', 'Drone', 'Smartphone Gimbal', 'Portable Projector', 'Smart Light Bulb', 'Smart Watch'],
          gadgets: ['Smart Watch', 'Wireless Charger', 'Action Camera', 'Fitness Tracker', 'Drone', 'Smartphone Gimbal', 'Portable Projector', 'Smart Light Bulb']
        };
        const allowedNames = categoryMap[selectedCategory.value] || [];
        filtered = filtered.filter(p => allowedNames.includes(p.name));
      }

      if (searchQuery.value.trim() !== '') {
        const query = searchQuery.value.toLowerCase();
        filtered = filtered.filter(p =>
          p.name.toLowerCase().includes(query) || p.description.toLowerCase().includes(query)
        );
      }

      if (sortBy.value) {
        if (sortBy.value === 'Price: Low to High') {
          filtered = [...filtered].sort((a, b) => a.price - b.price);
        } else if (sortBy.value === 'Price: High to Low') {
          filtered = [...filtered].sort((a, b) => b.price - a.price);
        } else if (sortBy.value === 'Name: A-Z') {
          filtered = [...filtered].sort((a, b) => a.name.localeCompare(b.name));
        } else if (sortBy.value === 'Name: Z-A') {
          filtered = [...filtered].sort((a, b) => b.name.localeCompare(a.name));
        }
      }

      return filtered;
    });

    const paginatedProducts = computed(() => {
      const start = (currentPage.value - 1) * perPage.value;
      const end = start + perPage.value;
      return filteredAndSortedProducts.value.slice(start, end);
    });

    const totalPages = computed(() => {
      return Math.ceil(filteredAndSortedProducts.value.length / perPage.value);
    });

    function changePage(page) {
      if (page < 1 || page > totalPages.value) return;
      currentPage.value = page;
    }

    watch([selectedCategory, sortBy, searchQuery], () => {
      currentPage.value = 1;
    });

    return{
      currentPage,
      perPage,
      paginatedProducts,
      totalPages,
      changePage,
      totalProducts: products.length,
      selectedCategory,
      sortBy,
      searchQuery
    }
  }
}
</script>

<style scoped>
  .select-wrapper{
    width: 200px;
  }
  .select-wrapper .icon{
    top: 12px;
  }
</style>