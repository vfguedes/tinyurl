<template>
  <Container>
    <h1 class="text-4xl font-bold text-green-400 title-border">tinyurl</h1>

    <Form class="my-8" />
  </Container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({})
</script>

<style lang="postcss" scoped>
.title-border {
  width: calc(100% - 16px);
  @apply border-b-2 border-green-300 pb-1;
}
</style>
