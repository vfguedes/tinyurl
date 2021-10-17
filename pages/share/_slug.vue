<template>
  <Container>
    <Title />

    <div class="flex items-center justify-center my-8 space-x-4">
      <div class="flex flex-col items-center justify-between h-full space-y-2">
        <a :href="'/' + slug" class="text-gray-800 underline" target="__blank">
          your link
        </a>
        <Button type="button" @button:click="copyToClipboard">copy 📋</Button>
      </div>
      <qrcode-vue :value="`${documentLocation}/${slug}`" foreground="#1F2937" />
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
      slug: this.$route.params.slug,
      documentLocation: document.location.origin,
    }
  },
  methods: {
    copyToClipboard() {
      navigator.clipboard.writeText(`${this.documentLocation}/${this.slug}`)
    },
  },
})
</script>
