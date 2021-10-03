<template>
  <Container>
    <h1 class="text-4xl font-bold text-green-400 title-border">tinyurl</h1>

    <Form v-if="!slug" class="my-8" @form:submit="updateSlug" />

    <div v-if="slug" class="flex items-center justify-center my-8 space-x-4">
      <div class="flex flex-col items-center justify-between h-full space-y-2">
        <a :href="slug" class="text-gray-800 underline" target="__blank"
          >your link</a
        >
        <Button type="button" @button:click="copyToClipboard">copy 📋</Button>
      </div>
      <qrcode-vue :value="slug" foreground="#1F2937"></qrcode-vue>
    </div>
  </Container>
</template>

<script lang="ts">
import Vue from 'vue'
import QrcodeVue from 'qrcode.vue'

export default Vue.extend({
  components: {
    QrcodeVue,
  },
  data() {
    return {
      slug: '',
    }
  },
  methods: {
    updateSlug(value: string) {
      this.slug = document.URL + value
    },
    copyToClipboard() {
      navigator.clipboard.writeText(`${document.URL}/${this.slug}`)
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
