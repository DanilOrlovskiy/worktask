<template>
  <div class="flex items-center mt-12 justify-between border-t border-white/10 px-4 py-3 sm:px-6">
    <div class="flex flex-1 justify-between sm:hidden">
      <a href="#"
         class="relative inline-flex items-center rounded-md border border-white/10 bg-white/5 px-4 py-2 text-sm font-medium text-gray-200 hover:bg-white/10">Previous</a>
      <a href="#"
         class="relative ml-3 inline-flex items-center rounded-md border border-white/10 bg-white/5 px-4 py-2 text-sm font-medium text-gray-200 hover:bg-white/10">Next</a>
    </div>
    <div class="hidden sm:flex sm:flex-1 sm:items-center sm:justify-between">
      <div>
        <p class="text-sm text-gray-300">
          Showing
          {{ ' ' }}
          <span class="font-medium">{{pageData.from}}</span>
          {{ ' ' }}
          to
          {{ ' ' }}
          <span class="font-medium">{{pageData.to}}</span>
          {{ ' ' }}
          of
          {{ ' ' }}
          <span class="font-medium">{{totalProducts}}</span>
          {{ ' ' }}
          results
        </p>
      </div>
      <div>
        <nav class="isolate inline-flex -space-x-px rounded-md" aria-label="Pagination">
          <a @click="changePage(currentPage - 1)"
             class="relative inline-flex items-center rounded-l-md px-2 py-2 text-gray-400 inset-ring inset-ring-gray-700 hover:bg-white/5 focus:z-20 focus:outline-offset-0">
            <span class="sr-only">Previous</span>
            <ChevronLeftIcon class="size-5" aria-hidden="true"/>
          </a>
          <a v-for="page in totalPages"
             :key="page"
             @click="changePage(page)"
             aria-current="page"
             :class="[
                'px-3 py-1 rounded-md border border-gray-300 hover:bg-gray-200',
                currentPage === page ? 'bg-indigo-600 text-white border-indigo-600' : 'text-gray-600'
              ]" >
            {{page}}
          </a>
          <a @click="changePage(currentPage + 1)"
             class="relative inline-flex items-center rounded-r-md px-2 py-2 text-gray-400 inset-ring inset-ring-gray-700 hover:bg-white/5 focus:z-20 focus:outline-offset-0">
            <span class="sr-only">Next</span>
            <ChevronRightIcon class="size-5" aria-hidden="true"/>
          </a>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
import { ChevronLeftIcon, ChevronRightIcon } from '@heroicons/vue/20/solid'
import {computed, reactive, ref} from "vue";

export default {
  name: "Pagination",
  components: {
    ChevronLeftIcon,
    ChevronRightIcon
  },
  props:{
    totalPages: {
      type: Number,
      required: true
    },
    totalProducts: {
      type: Number,
      default: null
    },
    perPage: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },
  emits: ['pageChanged'],
  setup(props, ctx){
    const totalPages = computed(() => props.totalPages);
    const pageData = reactive(
        {
          perPage: props.perPage,
          from: 1,
          to: props.perPage
        }
    );

    function setPerPageData(page){
      pageData.from = (page - 1) * pageData.perPage + 1;
      pageData.to = Math.min(page * pageData.perPage, props.totalProducts);
    }

    function changePage(page){
      ctx.emit('pageChanged', page)
      setPerPageData(page);
    }

    return{
      totalPages,
      totalProducts: props.totalProducts,
      pageData,
      changePage,
      currentPage: computed(() => {
        return props.currentPage;
      })
    }
  }
}
</script>

<style scoped>

</style>