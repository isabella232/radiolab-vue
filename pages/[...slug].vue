<script setup>
import { onBeforeMount, ref } from 'vue'
import axios from 'axios'
import SkeletonGeneralContent from '~/components/SkeletonGeneralContent.vue'
useMeta({
  bodyAttrs: {
    class: 'has-head-color',
  },
})
const dataLoaded = ref(false)
const page = ref([])
const route = useRoute()

onBeforeMount(async () => {
  await axios
    .get(
      `https://private-anon-26d14f4b2b-nyprpublisher.apiary-proxy.com/api/v3/channel/shows/radiolab/${route.params.slug}/1?limit=1`
    )
    .then((response) => {
      if (response.data.included.length < 1) {
        throwError('404')
      }
      page.value = response.data.included[0].attributes
      dataLoaded.value = true
    })
    .catch((error) => {
      throwError(error.response.status)
    })
})
</script>

<template>
  <div>
    <section class="head-color yellow">
      <div class="content thin-content-width">
        <template v-if="dataLoaded">
          <Html>
            <Head>
              <Title>{{ page.title }} | Radiolab | WNYC Studios</Title>
              <Meta
                name="og:title"
                :content="`${page.title} | Radiolab | WNYC Studios`"
              />
              <Meta
                name="twitter:title"
                :content="`${page.title} | Radiolab | WNYC Studios`"
              />
            </Head>
          </Html>
          <div class="html-formatting" v-html="page.body" />
        </template>
        <skeleton-general-content v-else />
      </div>
    </section>
  </div>
</template>

<style lang="scss" scoped>
h1 {
  font-size: var(--font-size-16);
}
</style>
