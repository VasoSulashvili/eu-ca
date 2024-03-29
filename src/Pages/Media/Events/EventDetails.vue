<template>
  <b-container>
    <loading-spinner v-if="loading" />
    <server-error v-if="errored" />
    <div v-if="!errored && !loading">
      <h4 style="max-width: 80%">{{ data[`title_${locale}`] }}</h4>
      <h5>
        {{
          data.date &&
            data.date
              .split(' ')[0]
              .split('-')
              .reverse()
              .join('.')
        }}
      </h5>
      <!-- <vue-pure-lightbox
        v-if="images.length"
        :thumbnail="images[0]"
        :images="images"
      ></vue-pure-lightbox>-->
      <div v-if="images.length" class="image-count">
        <div class="p-3">{{ images.length }} {{ $t('ItemsInGallery') }}</div>
      </div>
      <vue-markdown
        class="mt-3"
        :source="data[`article_${locale}`]"
      ></vue-markdown>
      <b-row>
        <b-col
          cols="3"
          class="pr-0"
          style="max-height: 200px; overflow: hidden"
          v-for="image in images"
          :key="image"
        >
          <vue-pure-lightbox
            style="width: 100%"
            :thumbnail="image"
            :images="[image]"
          ></vue-pure-lightbox>
        </b-col>
      </b-row>
      <div class="mt-3" v-if="data.video">
        <youtube
          player-width="300"
          player-height="180"
          :video-id="data.video && data.video.split('=')[1]"
        ></youtube>
      </div>
    </div>
  </b-container>
</template>

<script>
import VueMarkdown from 'vue-markdown';
import i18n from '@/plugins/i18n';
import { EVENTS_URL, API_BASE_URL } from '@/constants.js';
import LoadingSpinner from '@/components/LoadingSpinner';
import ServerError from '@/components/ServerError';
import VuePureLightbox from 'vue-pure-lightbox';

export default {
  name: 'Events',
  data() {
    return {
      data: null,
      images: null,
      more: null,
      loading: true,
      errored: false,
      API_BASE_URL,
      id: this.$route.params.id,
    };
  },
  computed: {
    locale: () => {
      return i18n.locale;
    },
  },
  mounted() {
    this.$http
      .get(EVENTS_URL + '/' + this.$route.params.id)
      .then(response => {
        this.data = response.data;
        this.images = response.data.photo_gallery.map(photo => {
          const image = `${API_BASE_URL}/uploads/${photo.hash}${photo.ext}`;
          return image;
        });
        this.images.push(
          `${API_BASE_URL}/uploads/${response.data.cover_image.hash}${response.data.cover_image.ext}`
        );
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  components: { LoadingSpinner, ServerError, VuePureLightbox, VueMarkdown },
};
</script>

<style lang="postcss" scoped>
.card-body {
  padding: 0;
}
.image-count {
  text-align: right;
  margin-top: -56px;
  color: #fff;
}
.image-count > div {
  display: inline-block;
  background: #00000099;
}
.card-title,
.card-text {
  padding: 10px;
  padding-top: 0;
}
.card-title {
  padding-top: 10px;
}
.card-text {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.date-container {
  /* background: #b74f29; */
  width: 100%;
  height: 100%;
  color: #1eaddd;
  font-weight: bold;
  font-size: 18px;
  position: relative;
  line-height: 16px;
}
.date-wrapper {
  width: 100%;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 30px;
}
.date-wrapper > div {
  border-left: 3px solid #1a61a7;
  display: flex;
  justify-items: center;
  flex-direction: column;
}
.lightbox__thumbnail img {
  min-height: 300px !important;
  max-height: 300px !important;
}
</style>
