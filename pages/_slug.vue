<!--  eslint-disable vue/valid-template-root -->
<template></template>

<script lang="ts">
import Vue from 'vue'
import { database } from '@/services/firebase'

export default Vue.extend({
  async beforeMount() {
    const slug = this.$nuxt.context.params.slug

    const linkRef = await database.ref(`links/${slug}`).get()

    if (linkRef.exists()) {
      const { url } = linkRef.val() as { url: string }

      if (url.includes('http') || url.includes('https')) {
        window.location.href = url
        return
      }

      window.location.href = 'https://' + url
    }
  },
})
</script>
