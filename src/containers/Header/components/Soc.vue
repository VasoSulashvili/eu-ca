<template>
  <div>
    <div>
      <b-input-group class="input-search" size="sm" style="width: 90%;">
        <b-form-input v-model="searchQuery" placeholder="Search"></b-form-input>
        <b-input-group-append>
          <b-button
            :disabled="!searchQuery"
            @click="search()"
            class="ml-0"
            variant="info"
          >
            <font-awesome-icon
              class="icon-search mr-1"
              :icon="['fas', 'search']"
            />
          </b-button>
        </b-input-group-append>
      </b-input-group>
    </div>
    <social-component />
    <!-- <div
      class="language-toggler"
      v-for="entry in languages"
      :key="entry.title"
      @click="changeLocale(entry.language)"
      v-show="entry.language !== i18n.locale"
    >
      <flag :iso="entry.flag" v-bind:squared="false"></flag>
    </div>-->
  </div>
</template>

<script>
import i18n from '@/plugins/i18n';
import LinksSeparator from '@/components/LinksSeparator';
import SocialComponent from './Social';
import router from '@/router';

export default {
  name: 'Language',
  methods: {
    handleClick: () => {},
    watch: {
      isSidebarOn: function(id) {
        console.log('changed', id);
      },
      deep: true,
    },
    search() {
      router.replace(`/search/${this.searchQuery}`);
      this.searchQuery = '';
      window.isSidebarclosed = true;
    },
    changeLocale(locale) {
      i18n.locale = locale;
      localStorage.setItem('activeLocale', locale);
      if (this.searchQuery && this.$router.currentRoute.name === 'search') {
        router.replace(`/search/${this.searchQuery}`);
      }
    },
    print() {
      window.print();
    },
  },
  components: {
    LinksSeparator,
    SocialComponent,
  },
  data() {
    return {
      searchQuery: '',
      languages: [
        { flag: 'gb', language: 'en', title: 'English' },
        { flag: 'ge', language: 'ge', title: 'ქართული' },
      ],
      i18n,
    };
  },
  created() {},
  destroyed() {},
};
</script>

<style lang="postcss" scoped>
.language {
  float: right;
  margin-top: 15px;
}

.language a {
  margin-left: 12px;
}

.language-toggler {
  cursor: pointer;
  display: inline-block;
  margin-left: 20px;
}

.icon-link,
.icon-sitemap,
#print-button {
  color: #2a3f70;
}

#print-button {
  background: none;
  border: none;
  padding: 2px;
}

#print-button:active,
#print-button:focus {
  color: #2a3f70;
  background: none;
  border: none !important;
  box-shadow: none;
}

.links {
  color: #2a3f70;
}

.links:hover {
  color: #1eaddd;
}
.input-search {
  margin-left: 20px;
  margin-top: 20px;
}
.input-search > input,
.input-search > .input-group-append > .btn {
  border-radius: 0;
}
.input-search > .input-group-append > .btn {
  background: #1eaddd !important;
  border-color: #1eaddd !important;
}
</style>
