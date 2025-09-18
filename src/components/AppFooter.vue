<template>
  <footer class="bg-gray-900 text-gray-400">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="flex flex-col md:flex-row items-center justify-between gap-6">
        <div class="flex items-center gap-2">
          <img class="h-8 w-auto" src="../../public/logo.png" alt="Your Company" />
        </div>

        <div class=" flex-grow sm:ml-6">
          <div class="flex justify-end space-x-4">
            <a v-for="item in navigation"
               :key="item.name"
               :href="item.href"
               :class="[item.current ? 'bg-gray-950/50 text-white' : 'text-gray-300 hover:bg-white/5 hover:text-white', 'rounded-md px-3 py-2 text-sm font-medium']"
               :aria-current="item.current ? 'page' : undefined"
            >
              {{ item.name }}
            </a>
          </div>
        </div>
      </div>

      <div class="mt-8 border-t border-gray-700 pt-6 text-sm text-gray-300 text-center md:text-left">
        <p>&copy; 2025 Volty. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script>
import {reactive} from "vue";

export default {
  name: "AppFooter",
  setup(){
    const navigation = reactive([
      { name: 'Products', href: '#', current: false },
      { name: 'About us', href: '#', current: false },
      { name: 'Contacts', href: '#', current: false },
    ]);
    return{
      navigation
    }
  }
}
</script>

<style lang="scss" scoped>

</style>