<template>
  <div class="social">
    <ul class="social-container">
      <li>
        <a
          class="btn-social fb"
          href="https://www.facebook.com/GeorgianNationalCompetitionAgency/"
          title="Facebook"
          target="_blank"
        >
          <font-awesome-icon class="fa" :icon="['fab', 'facebook']" />
        </a>
      </li>
      <li>
        <a
          class="btn-social twitter"
          href="https://twitter.com/gnc_agency/"
          title="Twitter"
          target="_blank"
        >
          <font-awesome-icon class="fa" :icon="['fab', 'twitter']" />
        </a>
      </li>
      <li>
        <a
          class="btn-social linkedin"
          href="https://www.linkedin.com/company/18127183/admin/"
          title="LinkedIn"
          target="_blank"
        >
          <font-awesome-icon class="fa" :icon="['fab', 'linkedin']" />
        </a>
      </li>
      <li>
        <a
          class="btn-social youtube"
          href="https://www.youtube.com/channel/UCS6PSHW37QIJxqiCBwm-YfQ"
          title="Youtube"
          target="_blank"
        >
          <font-awesome-icon class="fa" :icon="['fab', 'youtube']" />
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import headerLogo from '@/assets/logo.png';

export default {
  name: 'Social',
  components: {},
  data() {
    return {
      headerLogo,
    };
  },
};
</script>

<style lang="postcss" scoped>
.social-container {
  display: flex;
  margin-top: 19px;
  float: right;
}

.btn-social {
  padding: 3px 5px;
  text-align: center;
  color: #fff !important;
}
.btn-social.fb {
  background: #405d9b;
}
.btn-social.twitter {
  background: #1da1f2;
}
.btn-social.linkedin {
  background: #0177af;
}
.btn-social.instagram {
  background: #b60861;
}
.btn-social.youtube {
  background: #f01111;
}
.btn-social.fb:hover {
  background: #405d9bcc;
}
.btn-social.twitter:hover {
  background: #1da1f2cc;
}
.btn-social.instagram:hover {
  background: #b60861cc;
}
.btn-social.linkedin:hover {
  background: #0177afcc;
}
.btn-social.youtube:hover {
  background: #f01111cc;
}

@media screen and (max-width: 992px) {
  .social-container {
    display: flex;
    float: none;
    margin: 20px;
  }

  .btn-social {
    padding: 10px 15px;
    margin-right: 10px;
    text-align: center;
    color: #fff !important;
    border-radius: 50%;
  }
}
</style>
