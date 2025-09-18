<template>
  <Disclosure as="nav" class="relative bg-gray-800/50 after:pointer-events-none after:absolute after:inset-x-0 after:bottom-0 after:h-px after:bg-white/10">
    <div class="mx-auto max-w-7xl px-2 py-2 sm:px-6 lg:px-8">
      <div class="relative flex h-16 items-center justify-between">
        <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
          <!-- Mobile menu button-->
          <DisclosureButton class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-white/5 hover:text-white focus:outline-2 focus:-outline-offset-1 focus:outline-gray-500">
            <span class="absolute -inset-0.5" />
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!isOpen" class="block size-6" aria-hidden="true" />
            <XMarkIcon v-else class="block size-6" aria-hidden="true" />
          </DisclosureButton>
        </div>
        <div class="flex flex-1 items-center align-center justify-center h-full sm:justify-start">
          <div class="flex h-full shrink-0 items-center">
            <img class="h-full py-3 w-auto" src="../../public/logo.png" alt="Your Company" />
          </div>
          <div class=" flex-grow sm:ml-6 hidden md:block">
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
        <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
          <button type="button" class="relative rounded-full p-1 text-gray-400 hover:text-white focus:outline-2 focus:outline-offset-2 focus:outline-gray-500">
            <span class="absolute -inset-1.5" />
            <span class="sr-only">View notifications</span>
            <BellIcon class="size-6" aria-hidden="true" />
          </button>

          <!-- Profile dropdown -->
          <Menu as="div" class="relative ml-3">
            <MenuButton class="relative flex rounded-full focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-gray-500">
              <span class="absolute -inset-1.5" />
              <span class="sr-only">Open user menu</span>
              <svg class="size-6 user-circle-icon text-gray-400 hover:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" d="M17.982 18.725A7.488 7.488 0 0 0 12 15.75a7.488 7.488 0 0 0-5.982 2.975m11.963 0a9 9 0 1 0-11.963 0m11.963 0A8.966 8.966 0 0 1 12 21a8.966 8.966 0 0 1-5.982-2.275M15 9.75a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
              </svg>
            </MenuButton>

            <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform scale-100" leave-to-class="transform opacity-0 scale-95">
              <MenuItems class="absolute right-0 z-10 mt-2 w-48 origin-top-right rounded-md bg-gray-800 py-1 outline -outline-offset-1 outline-white/10">
                <MenuItem>
                  <a href="#" :class="[active ? 'bg-white/5 outline-hidden' : '', 'block px-4 py-2 text-sm text-gray-300']">Your profile</a>
                </MenuItem>
                <MenuItem>
                  <a href="#" :class="[active ? 'bg-white/5 outline-hidden' : '', 'block px-4 py-2 text-sm text-gray-300']">Settings</a>
                </MenuItem>
                <MenuItem>
                  <a href="#" :class="[active ? 'bg-white/5 outline-hidden' : '', 'block px-4 py-2 text-sm text-gray-300']">Sign out</a>
                </MenuItem>
              </MenuItems>
            </transition>
          </Menu>
        </div>
      </div>
    </div>

    <DisclosurePanel class="sm:hidden">
      <div class="space-y-1 px-2 pt-2 pb-3">
        <DisclosureButton v-for="item in navigation" :key="item.name" as="a" :href="item.href" :class="[item.current ? 'bg-gray-950/50 text-white' : 'text-gray-300 hover:bg-white/5 hover:text-white', 'block rounded-md px-3 py-2 text-base font-medium']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</DisclosureButton>
      </div>
    </DisclosurePanel>
  </Disclosure>
</template>

<script>
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { Bars3Icon, BellIcon, XMarkIcon } from '@heroicons/vue/24/outline'
import { UserCircleIcon } from '@heroicons/vue/20/solid';
import {reactive, ref} from "vue";

export default {
  name: "AppHeader",
  components: {
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    Bars3Icon,
    BellIcon,
    XMarkIcon,
    UserCircleIcon
  },
  setup(){
    const navigation = reactive([
      { name: 'Home', href: '#', current: false },
      { name: 'Products', href: '#', current: true },
      { name: 'About us', href: '#', current: false },
      { name: 'Contacts', href: '#', current: false },
    ]);
    const isOpen = ref(false);
    const active = ref(false);

    return{
      navigation,
      isOpen,
      active
    }
  }
}
</script>

<style scoped>
 .user-circle-icon path{

 }
</style>