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
              <ChevronDownIcon class="icon col-start-1 row-start-1 size-5 self-center justify-self-end text-gray-400 absolute sm:size-4" aria-hidden="true" />
            </ListboxButton>
            <transition leave-active-class="transition ease-in duration-100" leave-from-class="" leave-to-class="opacity-0">
              <ListboxOptions class="absolute z-10 mt-1 max-h-56 w-full overflow-auto border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm sm:text-sm">
                <ListboxOption as="template" :value="'All Categories'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">All Categories</span>
                    </div>
                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'audio'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Audio</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'computers'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Computers</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'gadgets'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Gadgets</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
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
              <ChevronDownIcon class="icon col-start-1 row-start-1 size-5 self-center justify-self-end text-gray-400 absolute sm:size-4" aria-hidden="true" />
            </ListboxButton>
            <transition leave-active-class="transition ease-in duration-100" leave-from-class="" leave-to-class="opacity-0">
              <ListboxOptions class="absolute z-10 mt-1 max-h-56 w-full overflow-auto border border-gray-300 rounded-xl px-3 py-2 text-sm bg-white text-gray-700 shadow-sm sm:text-sm">
                <ListboxOption as="template" :value="'Sort By'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Sort By</span>
                    </div>
                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Price: Low to High'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Price: Low to High</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Price: Low to High'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Price: Low to High</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Name: A-Z'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Name: A-Z</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                    <CheckIcon class="size-5" aria-hidden="true" />
                  </span>
                  </li>
                </ListboxOption>
                <ListboxOption as="template" :value="'Name: Z-A'" v-slot="{ active, selected }">
                  <li :class="[active ? 'bg-gray-500 text-white outline-hidden' : 'text-white', 'relative cursor-default py-2 pr-9 pl-3 select-none']">
                    <div class="flex items-center">
                      <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-3 block truncate']">Name: Z-A</span>
                    </div>

                    <span v-if="selected" :class="[active ? 'text-white' : 'text-gray-400', 'absolute inset-y-0 right-0 flex items-center pr-4']">
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
              class="w-full h-56 object-cover"
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
import { Listbox, ListboxButton, ListboxLabel, ListboxOption, ListboxOptions } from '@headlessui/vue'
import { ChevronDownIcon } from '@heroicons/vue/20/solid'
import { CheckIcon } from '@heroicons/vue/20/solid'
import { reactive, ref, computed, watch } from 'vue'
import Pagination from "./Pagination.vue";

export default {
  name: "ProductGrid",
  components: {Listbox, ListboxButton, ListboxLabel, ListboxOption, ListboxOptions, Pagination, ChevronDownIcon, CheckIcon},
  setup(){
    const products = reactive([
      { id: 1, name: 'Wireless Headphones', description: 'Noise-cancelling over-ear headphones', price: 99.99, image: 'https://via.placeholder.com/300x200?text=Headphones' },
      { id: 2, name: 'Smart Watch', description: 'Track your activity and notifications', price: 149.99, image: 'https://via.placeholder.com/300x200?text=Smart+Watch' },
      { id: 3, name: 'Bluetooth Speaker', description: 'Portable speaker with deep bass', price: 59.99, image: 'https://via.placeholder.com/300x200?text=Speaker' },
      { id: 4, name: 'Gaming Mouse', description: 'High precision RGB mouse', price: 39.99, image: 'https://via.placeholder.com/300x200?text=Gaming+Mouse' },
      { id: 5, name: 'Mechanical Keyboard', description: 'RGB backlit mechanical keyboard', price: 79.99, image: 'https://via.placeholder.com/300x200?text=Keyboard' },
      { id: 6, name: 'Laptop Stand', description: 'Ergonomic aluminum laptop stand', price: 29.99, image: 'https://via.placeholder.com/300x200?text=Laptop+Stand' },
      { id: 7, name: 'HD Webcam', description: '1080p USB webcam for video calls', price: 49.99, image: 'https://via.placeholder.com/300x200?text=Webcam' },
      { id: 8, name: 'External SSD', description: 'Fast portable 1TB SSD', price: 129.99, image: 'https://via.placeholder.com/300x200?text=External+SSD' },
      { id: 9, name: 'Wireless Charger', description: 'Qi-certified fast charger', price: 19.99, image: 'https://via.placeholder.com/300x200?text=Wireless+Charger' },
      { id: 10, name: 'Action Camera', description: '4K waterproof action camera', price: 199.99, image: 'https://via.placeholder.com/300x200?text=Action+Camera' },
      { id: 11, name: 'Fitness Tracker', description: 'Track steps and sleep patterns', price: 49.99, image: 'https://via.placeholder.com/300x200?text=Fitness+Tracker' },
      { id: 12, name: 'Drone', description: 'Quadcopter with HD camera', price: 299.99, image: 'https://via.placeholder.com/300x200?text=Drone' },
      { id: 13, name: 'Smartphone Gimbal', description: 'Stabilizer for smooth videos', price: 89.99, image: 'https://via.placeholder.com/300x200?text=Gimbal' },
      { id: 14, name: 'Portable Projector', description: 'Mini projector for movies', price: 159.99, image: 'https://via.placeholder.com/300x200?text=Projector' },
      { id: 15, name: 'Noise Cancelling Earbuds', description: 'True wireless earbuds', price: 79.99, image: 'https://via.placeholder.com/300x200?text=Earbuds' },
      { id: 16, name: 'Smart Light Bulb', description: 'WiFi-controlled RGB bulb', price: 24.99, image: 'https://via.placeholder.com/300x200?text=Smart+Bulb' }
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