<template>
  <div :class="{ 'flex flex-col': error }">
    <input
      :value="value"
      :type="type"
      :placeholder="placeholder"
      :class="{
        'border-red-400 focus:ring-red-500 hover:border-red-600': error,
      }"
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
        w-full
      "
      @input="$emit('input:update', $event.target.value)"
    />

    <span v-if="error" class="text-sm text-red-400">{{ error }}</span>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  props: {
    value: {
      type: String,
      required: false,
      default: '',
    },
    type: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: true,
    },
    error: {
      type: String,
      required: false,
      default: '',
    },
  },
})
</script>
