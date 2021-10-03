<template>
  <div
    class="
      w-64
      h-screen
      mx-auto
      my-auto
      flex flex-col
      items-center
      justify-center
    "
  >
    <h1 class="text-4xl font-bold text-green-400 title-border">tinyurl</h1>

    <form class="flex flex-col space-y-4 my-8" @submit.prevent="submit">
      <input
        v-model="url"
        type="text"
        placeholder="url"
        class="
          p-2
          rounded
          text-gray-800
          border border-gray-200
          hover:border-gray-400
          focus:outline-none
          focus:ring
          focus:ring-opacity-50
          focus:ring-green-500
          focus:border-transparent
          transition-all
          duration-150
        "
      />
      <input
        v-model="slug"
        type="text"
        placeholder="slug (optional)"
        class="
          p-2
          rounded
          text-gray-800
          border border-gray-200
          hover:border-gray-400
          focus:outline-none
          focus:ring
          focus:ring-opacity-50
          focus:ring-green-500
          focus:border-transparent
          transition-all
          duration-150
        "
      />
      <button
        type="submit"
        class="
          px-4
          py-2
          rounded
          text-white
          bg-green-500
          hover:bg-green-600 hover:underline
          focus:outline-none
          focus:ring
          focus:ring-opacity-50
          focus:ring-green-500
          transition-all
          duration-150
        "
      >
        generate link 🔗
      </button>
    </form>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { validateURL } from '@/utils/validate-url'

export default Vue.extend({
  data() {
    return {
      url: '',
      slug: '',
    }
  },
  methods: {
    submit() {
      console.log('url: ' + this.url, 'slug: ' + this.slug)

      if (!validateURL(this.url)) {
        alert('Invalid URL')
      }
    },
  },
})
</script>

<style lang="postcss" scoped>
.title-border {
  width: calc(100% - 16px);
  @apply border-b-2 border-green-300 pb-1;
}
</style>
