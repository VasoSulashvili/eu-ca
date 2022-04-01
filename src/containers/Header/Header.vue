<template>
  <b-container>
    <!-- <div
      style="padding: 10px; font-size: 16px; color: red; font-weight: bold; text-align: center; width: 100%"
    >{{ $t("TESTVERSION") }}</div> -->
    <div class="app-top-header hidden-print">
      <div class="header-left">
        <logo-component />
        <div class="euca-title">
          <div class="header-logo-title">
            <span>{{ logoTitle }}</span>
          </div>
        </div>
      </div>
      <span class="lang-social">
        <language-component />
      </span>
    </div>
    <div class="header mobile" style="position: relative">
      <logo-component />
      <mobile-language-component />
    </div>
  </b-container>
</template>

<script>
import i18n from '@/plugins/i18n';
import LogoComponent from './components/Logo';
import SocialComponent from './components/Social';
import LanguageComponent from './components/Language';
import MobileLanguageComponent from './components/Lang';

console.log(i18n.locale == 'ge');
export default {
  name: 'Header',
  components: {
    LogoComponent,
    SocialComponent,
    LanguageComponent,
    MobileLanguageComponent,
  },
  computed: {
    logoTitle() {
      let title =
        i18n.locale == 'ge'
          ? ' საქართველოს\nკონკურენციის\nეროვნული სააგენტო'
          : i18n.locale == 'en'
          ? `Georgia National\nCompetition\nAgency`
          : '';
      return title.trim();
    },
  },
  data() {
    return {};
  },
};
</script>

<style lang="postcss" scoped>
.header-logo-title {
  border-left: 2px solid #1a61a7;
  padding-left: 5px;
  max-width: none;
  margin-bottom: 10px;
  /* font-family: 'Open Sans', 'BPG Glaho WEB Caps', sans-serif; */
  color: #1a61a7;
  font-size: 18px;
  text-align: left;
}
.header-logo-title span {
  white-space: pre;
}
.app-top-header {
  margin: 20px 0;
  position: relative;
}

.euca-title {
  display: inline;
  margin-left: 110px;
}

.header-left {
  display: flex;
  position: relative;
}

.euca-title {
  position: absolute;
  transform: translateY(-50%);
  top: 50%;
}

.euca-title div {
  font-size: 16px;
  display: inline-block;
}

.lang-social {
  position: absolute;
  right: 0;
  top: 0;
}

/* 
@media (max-width: 1200px) {
  
} */

@media (max-width: 992px) {
  .lang-social {
    display: none;
  }

  .header-left {
    display: none;
  }
}
</style>
