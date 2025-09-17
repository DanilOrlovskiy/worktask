<template>
  <section class="py-12 relative bg-gray-800/50 after:pointer-events-none after:absolute after:inset-x-0 after:bottom-0 after:h-px after:bg-white/10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <h2 class="text-2xl font-bold text-gray-900 mb-6">Our Products</h2>

      <!-- Filters -->
      <div class="mb-6 flex flex-wrap items-center gap-4">
        <select v-model="selectedCategory" class="border border-gray-300 rounded-md px-3 py-2 text-sm focus:ring-indigo-500 focus:border-indigo-500">
          <option value="">All Categories</option>
          <option value="audio">Audio</option>
          <option value="computers">Computers</option>
          <option value="gadgets">Gadgets</option>
        </select>
        <select v-model="sortBy" class="border border-gray-300 rounded-md px-3 py-2 text-sm focus:ring-indigo-500 focus:border-indigo-500">
          <option value="">Sort By</option>
          <option value="price-asc">Price: Low to High</option>
          <option value="price-desc">Price: High to Low</option>
          <option value="name-asc">Name: A-Z</option>
          <option value="name-desc">Name: Z-A</option>
        </select>
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search products..."
          class="flex-1 border border-gray-300 rounded-md px-3 py-2 text-sm focus:ring-indigo-500 focus:border-indigo-500"
        />
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
            v-for="product in paginatedProducts"
            :key="product.id"
            class="flex flex-col flex-grow rounded-3xl rounded-t-3xl bg-white/2.5 p-6 ring-1 ring-white/10 sm:mx-8 sm:p-6 lg:mx-0 lg:rounded-bl-3xl"
        >
          <img
              :src="product.image"
              :alt="product.name"
              class="w-full h-56 object-cover"
          />
          <div class="flex flex-col flex-grow pt-4">
            <h3 class="text-lg font-semibold text-gray-900">{{ product.name }}</h3>
            <p class="flex-grow mt-2 text-gray-600 text-sm">{{ product.description }}</p>
            <div class="mt-4 flex items-center justify-between">
              <span class="text-indigo-600 font-bold">${{ product.price }}</span>
              <button
                  class="bg-indigo-600 text-white px-3 py-1 rounded hover:bg-indigo-700 transition"
              >
                Buy
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
import { reactive, ref, computed, watch } from 'vue'
import Pagination from "./Pagination.vue";

export default {
  name: "ProductGrid",
  components: {Pagination},
  setup(_, { emit }){
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
    const selectedCategory = ref('');
    const sortBy = ref('');
    const searchQuery = ref('');

    const filteredAndSortedProducts = computed(() => {
      let filtered = products;

      if (selectedCategory.value) {
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
        if (sortBy.value === 'price-asc') {
          filtered = [...filtered].sort((a, b) => a.price - b.price);
        } else if (sortBy.value === 'price-desc') {
          filtered = [...filtered].sort((a, b) => b.price - a.price);
        } else if (sortBy.value === 'name-asc') {
          filtered = [...filtered].sort((a, b) => a.name.localeCompare(b.name));
        } else if (sortBy.value === 'name-desc') {
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

</style>