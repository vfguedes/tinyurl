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
import { generate } from 'randomstring'
import { database } from '@/services/firebase'
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
    async submit() {
      const linksRef = database.ref('links')
      this.errors.url = ''
      this.errors.slug = ''

      if (!validateURL(this.url)) {
        this.errors.url = 'invalid url'
        return
      }

      if (this.slug) {
        const slugRef = await linksRef.child(this.slug).get()
        const slugExists = slugRef.exists()

        if (slugExists) {
          this.errors.slug = 'slug already used'
          return
        }

        linksRef.child(this.slug).set({
          url: this.url,
        })

        this.$emit('form:submit', this.slug)
        return
      }

      const generated = generate(7)

      linksRef.child(generated).set({
        url: this.url,
      })

      this.$emit('form:submit', generated)
    },
  },
})
</script>
