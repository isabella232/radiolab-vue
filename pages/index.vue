<script setup>
import { useRuntimeConfig } from '#app'
const config = useRuntimeConfig()
// const recentEpisodesApiUrl = `${ config.API_URL }/api/v3/channel/shows/radiolab/recent_stories/`
// const popularEpisodesApiUrl = `${ config.API_URL }/api/v3/channel/shows/radiolab/recent_stories/`
const recentEpisodesApiUrl = `https://private-anon-26d14f4b2b-nyprpublisher.apiary-proxy.com/api/v3/channel/shows/radiolab/recent_stories/`
const popularEpisodesApiUrl = `https://private-anon-26d14f4b2b-nyprpublisher.apiary-proxy.com/api/v3/channel/shows/radiolab/recent_stories/`
</script>

<template>
  <div>
    <latest-episode class="mb-4" />
    <episodes
      class="mb-4"
      header="Recent Episodes"
      button-text="All Episodes"
      button-link="/episodes"
      :row-count="1"
      :startCount="1"
      :api="recentEpisodesApiUrl"
      path="data.included"
    />
    <div class="htlad-radiolab_in-content_1 mb-8" />
    <exclusive-content-from-the-lab class="mb-8" />
    <section class="mb-8">
      <div class="content">
        <div class="grid">
          <div class="col-12 md:col-6">
            <subscribe-to-the-newsletter />
          </div>
          <div class="col-12 md:col-6">
            <listeners-cta />
          </div>
        </div>
      </div>
    </section>
    <radiolab-series class="mb-8" />
    <episodes
      class="mb-8"
      header="Popular Episodes"
      button-text="All Episodes"
      button-link="/episodes"
      :row-count="1"
      :startCount="1"
      :api="popularEpisodesApiUrl"
      path="data.included"
    />
    <div class="htlad-radiolab_in-content_2 mb-8" />
  </div>
</template>
