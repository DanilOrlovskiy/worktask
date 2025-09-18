<template>
  <footer class="bg-gray-900 text-gray-400">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <!-- Верхняя часть -->
      <div class="flex flex-col md:flex-row items-center justify-between gap-6">
        <!-- Логотип -->
        <div class="flex items-center gap-2">
          <img src="https://tailwindui.com/img/logos/mark.svg?color=gray&shade=500"
               alt="Logo"
               class="h-8 w-auto" />
          <span class="text-white font-semibold text-lg">MyCompany</span>
        </div>

        <!-- Навигация -->
        <nav class="flex gap-6 text-sm">
          <a href="#" class="hover:text-white transition">About</a>
          <a href="#" class="hover:text-white transition">Services</a>
          <a href="#" class="hover:text-white transition">Blog</a>
          <a href="#" class="hover:text-white transition">Contact</a>
        </nav>

        <!-- Соцсети -->
        <div class="flex gap-4">
          <a href="#" class="hover:text-white transition">
            <i class="fab fa-facebook-f"></i>
          </a>
          <a href="#" class="hover:text-white transition">
            <i class="fab fa-twitter"></i>
          </a>
          <a href="#" class="hover:text-white transition">
            <i class="fab fa-instagram"></i>
          </a>
        </div>
      </div>

      <!-- Нижняя часть -->
      <div class="mt-8 border-t border-gray-700 pt-6 text-sm text-center md:text-left">
        <p>&copy; 2025 MyCompany. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "AppFooter"
}
</script>

<style lang="scss" scoped>

</style>