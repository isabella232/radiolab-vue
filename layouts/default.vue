<script setup>
import { ref, onMounted } from 'vue'
import { useRuntimeConfig } from '#app'
const config = useRuntimeConfig()
const route = useRoute()
const darkMode = ref(false)
const atTop = ref(true)

onMounted(() => {
  document.addEventListener('scroll', (e) => {
    atTop.value = window.scrollY > 0 ? false : true
    //atBottom.value = ((window.scrollY + (window.innerHeight + 115) >= document.body.scrollHeight)) ? true : false
  })
  // Ads
  window.htlbid = window.htlbid || {}
  htlbid.cmd = htlbid.cmd || []
  htlbid.cmd.push(function () {
    htlbid.layout('universal') // Leave as 'universal' or add custom layout
    htlbid.setTargeting('is_testing', config.HTL_IS_TESTING) // Set to "no" for production
    htlbid.setTargeting('is_home', route.name === 'index' ? 'yes' : 'no') // Set to "yes" on the homepage
    htlbid.setTargeting('category', route.name) // dynamically pass page category into this function
    htlbid.setTargeting('post_id', route.name) // dynamically pass unique post/page id into this function
  })
})
</script>

<template>
  <div
    class="page"
    :class="[`${route.name}`]"
    :data-style-mode="darkMode ? 'dark' : 'default'"
  >
    <Html>
      <Head>
        <Link rel="stylesheet" :href="config.HTL_CSS" type="text/css" />
        <Script :src="config.HTL_JS" async />
        <Title>Radiolab: Podcasts | WNYC Studios | Podcasts</Title>
        <Meta name="description" content="Investigating a strange world." />
        <Meta
          name="keywords"
          content="podcasts, npr, new york, WNYC Studios, arts, culture, classical, music, news, public, radio"
        />
        <Meta name="og:site_name" content="Radiolab Podcasts | WNYC Studios" />
        <Meta name="og:type" content="website" />
        <Meta
          name="og:url"
          :content="`https://www.radiolab.org${route.fullPath}`"
        />
        <Meta
          name="og:title"
          content="Radiolab: Podcasts | WNYC Studios | Podcasts"
        />
        <Meta name="og:description" content="Investigating a strange world." />
        <Meta
          name="og:image"
          content="https://media.wnyc.org/i/1200/600/l/80/2020/09/Radiolab_OG_Image_Options_3.png"
        />
        <Meta name="og:image:width" content="1200" />
        <Meta name="og:image:height" content="600" />
        <Meta name="fb:app_id" content="151261804904925" />
        <Meta
          name="fb:pages"
          content="224921207956535"
          data-detail="WNYC Studios"
        />
        <Meta name="twitter:card" content="summary_large_image" />
        <Meta name="twitter:site" content="@radiolab" />
        <Meta
          name="twitter:title"
          content="Radiolab: Podcasts | WNYC Studios | Podcasts"
        />
        <Meta
          name="twitter:description"
          content="Investigating a strange world."
        />
        <Meta
          name="twitter:image"
          content="https://media.wnyc.org/i/1200/600/l/80/2020/09/Radiolab_OG_Image_Options_3.png"
        />
        <Meta
          name="apple-itunes-app"
          content="app-id=152249110, affiliate-data=at=1010lSme&amp;ct=radiolab"
        />
      </Head>
    </Html>
    <radiolab-header :class="[{ 'at-top': atTop }]" />
    <main>
      <slot />
    </main>
    <radiolab-footer />
    <audio-player />
  </div>
</template>

<style lang="scss">
body,
html {
  overflow-y: auto;
  overflow-x: hidden;
}

main {
  padding-top: var(--header-height);
}
</style>
