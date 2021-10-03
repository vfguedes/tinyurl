<template>
  <form class="flex flex-col space-y-4" @submit.prevent="submit">
    <Input
      type="text"
      placeholder="url"
      :value="url"
      :error="errors.url"
      @input:update="url = $event"
    />
    <Input
      type="text"
      placeholder="slug (optional)"
      :value="slug"
      :error="errors.slug"
      @input:update="slug = $event"
    />
    <Button type="submit">generate link 🔗</Button>
  </form>
</template>

<script lang="ts">
import Vue from 'vue'
import { validateURL } from '@/utils/validate-url'

export default Vue.extend({
  data() {
    return {
      url: '',
      slug: '',
      errors: {
        url: '',
        slug: '',
      },
    }
  },
  methods: {
    submit() {
      console.log('url: ' + this.url, 'slug: ' + this.slug)
      this.errors.url = ''
      this.errors.slug = ''

      if (!validateURL(this.url)) {
        this.errors.url = 'invalid url'
      }

      if (this.slug === 'abc') {
        this.errors.slug = 'slug already used'
      }
    },
  },
})
</script>
