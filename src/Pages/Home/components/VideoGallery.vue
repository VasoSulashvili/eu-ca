<template>
  <div class="cards">
    <a href="https://www.youtube.com/channel/UCS6PSHW37QIJxqiCBwm-YfQ" target="_blank"><h4 class="mb-2 section-title">{{ $t('VideoGallery') }}</h4></a>
      <b-row>
        <b-col lg="6" v-for="video in data" :key="video.id">
          <youtube player-width="100%" player-height="220" :video-id="video.link.split('=')[1]"></youtube>
          <div class="video-title">{{ video[`title_${locale}`] }}</div>
        </b-col>
      </b-row>

    <div style="width: 100%; text-align: right">
      <a class="btn-read-more" href="https://www.youtube.com/channel/UCS6PSHW37QIJxqiCBwm-YfQ" target="_blank">{{ $t("ViewAll") }}...</a>
    </div>
    <!-- {{ $t('VideoGallery') }} -->
    <!-- <div v-for="video in data" :key="video.id">
      {{ video[`title_${locale}`] }}
      <youtube :video-id="video.link.split('=')[1]"></youtube>
    </div>-->
  </div>
</template>

<script>
import i18n from '@/plugins/i18n';
import { API_BASE_URL, VIDEOS_URL } from '@/constants.js';

export default {
  name: 'VideoGallery',
  components: {},
  data() {
    return {
      i18n,
      API_BASE_URL: API_BASE_URL,
      data: null,
      loading: true,
      errored: false,
    };
  },
  computed: {
    locale: () => {
      return i18n.locale;
    },
    videos: () => {
      return (
        this.data.length &&
        this.data.map(video => {
          const parts = video.link.split('=');
          return parts[parts.length - 1];
        })
      );
    },
  },
  mounted() {
    this.$http
      .get(VIDEOS_URL)
      .then(response => {
        this.data = response.data.slice(0, 2);
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>

<style lang='postcss' scoped>

.video-title{
  font-size: 14px;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
</style>