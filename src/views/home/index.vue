<template>
  <header class="header">
    <img src="https://cdn.jsdelivr.net/gh/fonghehe/picture/vue-h5-template/logo.png" alt="" /><span> {{ $t('title') }}</span>
  </header>
  <div class="intro-header">
    <div>{{ $t('introduction') }}</div>
    <a href="https://github.com/sunniejs/vue-h5-template.git">
      <Github />
    </a>
  </div>
  <nut-cell-group :title="$t('home.support')" class="supportList">
    <nut-cell v-for="(item, index) in cellList" :key="index" :title="item">
      <template #icon>
        <Check />
      </template>
    </nut-cell>
  </nut-cell-group>
  <nut-cell-group :title="$t('home.cssMultiLanguage')" class="supportList">
    <nut-cell>
      <div :class="['btn-confirm', locale]"></div>
    </nut-cell>
  </nut-cell-group>
  <div class="btn-wrap">
    <nut-button shape="square" size="small" type="default" @click="changeLang('zh-cn')">
      {{ $t('language.zh') }}
    </nut-button>
    <nut-button shape="square" size="small" type="default" @click="changeLang('en-us')">
      {{ $t('language.en') }}
    </nut-button>
  </div>
</template>

<script lang="ts" setup name="HomePage">
  import { setLang } from '@/i18n';
  import { useI18n } from 'vue-i18n';
  import { Github, Check } from '@nutui/icons-vue';

  const { locale } = useI18n();

  const cellList = ['vue3', 'vite', 'vue-router', 'axios', 'Pinia', 'vue-i18n', 'postcss-px-to-viewport', 'varlet / vant / nutUI', 'eruda'];

  const changeLang = (type) => {
    setLang(type);
  };
</script>
<style lang="scss">
  @use '@/styles/mixin.scss' as *;

  .header {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 20px;
    font-size: 40px;

    img {
      width: 90px;
      height: 90px;
    }
  }

  .intro-header {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 20px;
    font-size: 24px;
  }

  .supportList {
    margin: 0 16px;

    .nut-cell-group__title {
      margin-top: 30px;
    }
  }

  .btn-wrap {
    margin: 20px;
  }

  .btn-confirm {
    @include main-lang-bg(302px, 82px, '@/assets/button', 'confirm.png');
  }
</style>
