<template>
  <b-container>
    <loading-spinner v-if="loading" />
    <server-error v-if="errored" />
    <div v-if="!errored && !loading">
      <div v-for="article in data" v-bind:key="article.id">
        <div>
          <b-card-group deck>
            <b-card
              :title="article[`title_${locale}`]"
              header-tag="header"
              footer-tag="footer"
              class="mb-3"
            >
              <h6 slot="header" class="mb-0 decision-date">{{ article.date.split(" ")[0] }}</h6>
              <b-card-text><vue-markdown :source="article[`article_${locale}`]"></vue-markdown></b-card-text>
              <b-button
                class="doc-button"
                :href="article[`document_${locale}`] && `${API_BASE_URL}/uploads/${article[`document_${locale}`].hash}${article[`document_${locale}`].ext}`"
                :disabled="!article[`document_${locale}`]"
              >{{ $t('ViewDocument') }}</b-button>
              <em slot="footer">
                <span
                  v-for="tag in article[`tags_${locale}`] && article[`tags_${locale}`].split('#')"
                  :key="tag"
                >
                  <router-link :to="`/search/${tag}`">#{{ tag }}</router-link>
                </span>
              </em>
            </b-card>
          </b-card-group>
        </div>
        <!-- <vue-simple-markdown :source="article.Tags"></vue-simple-markdown> -->
      </div>
    </div>
  </b-container>
</template>

<script>
import VueMarkdown from 'vue-markdown';
import i18n from '@/plugins/i18n';
import {
  API_BASE_URL,
  ABUSEOFDOMINITIONBYPROHIBITION_URL,
} from '@/constants.js';
import LoadingSpinner from '@/components/LoadingSpinner';
import ServerError from '@/components/ServerError';
import { sortArrayByDate } from '@/utils';

export default {
  name: 'ByProhibition',
  data() {
    return {
      data: null,
      loading: true,
      errored: false,
      API_BASE_URL,
    };
  },
  computed: {
    locale: () => {
      return i18n.locale;
    },
  },
  mounted() {
    this.$http
      .get(ABUSEOFDOMINITIONBYPROHIBITION_URL + '?_sort=date:DESC')
      .then(response => {
        this.data = sortArrayByDate(response.data.decisions);
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  components: { LoadingSpinner, ServerError, VueMarkdown },
};
</script>

<style lang="postcss" scoped>
.card {
  border-radius: 0 !important;
}

.doc-button {
  background: transparent;
  color: #db2323;
  border: none;
  padding: 0;
}

.doc-button:hover {
  color: #ff5d43;
}
</style>