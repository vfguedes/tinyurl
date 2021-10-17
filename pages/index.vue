<template>
  <Container>
    <Title />

    <Form class="my-8" @form:submit="redirectToSharePage" />
  </Container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  methods: {
    redirectToSharePage(slug: string) {
      this.$nuxt.$router.push(`share/${slug}`)
    },
  },
})
</script>
