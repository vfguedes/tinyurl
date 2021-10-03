<template>
  <button
    :type="type"
    class="
      px-4
      py-2
      rounded
      text-white
      bg-green-500
      hover:bg-green-600 hover:underline
      focus:outline-none focus:ring focus:ring-opacity-50 focus:ring-green-500
      transition-all
      duration-150
    "
    @click="$emit('button:click')"
  >
    <slot />
  </button>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  props: {
    type: {
      type: String,
      required: true,
    },
  },
})
</script>
