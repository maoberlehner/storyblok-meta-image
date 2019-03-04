<template>
  <div class="MetaImage image__wrap">
    <div
      v-if="model.src"
      class="uk-flex uk-flex-middle uk-margin-bottom"
    >
      <img
        class="image"
        :src="model.src.replace(`a.storyblok.com`, `img2.storyblok.com/40x30`)"
      >

      <div class="util__break-all">
        <a
          target="_blank"
          class="link link--inverse"
          :href="model.src"
        >
          {{ model.src.split(`/`).reverse()[0] }}
        </a>
        <a
          title="Remove"
          class="image__btn"
          @click="clear"
        >
          <i class="uk-icon-minus-circle"/>
        </a>
      </div>
    </div>
    <input
      class="uk-width-1-1 uk-margin-small-bottom"
      :value="model.src"
      readonly
    >
    <input
      v-model="model.title"
      type="text"
      class="uk-form-small assets__item-name"
      placeholder="Title"
    >
    <input
      v-model="model.alt"
      type="text"
      class="uk-form-small assets__item-name"
      placeholder="Alt"
    >
    <input
      v-model="model.dominant_color"
      type="text"
      class="uk-form-small assets__item-name"
      placeholder="Dominant color"
    >
    <sb-asset-selector
      :uid="uid"
      field="src"
      class="uk-button-small uk-margin-top"
    />
  </div>
</template>

<script>
import ColorThief from '../vendor/color-thief.min';
import rgb2hex from './utils/rgb2hex';

const initialValue = {
  alt: ``,
  dominant_color: ``,
  height: 0,
  plugin: `meta-image`,
  src: ``,
  title: ``,
  width: 0,
};

export default {
  mixins: [window.Storyblok.plugin],
  watch: {
    model: {
      deep: true,
      handler(value) {
        this.$emit(`changed-model`, value);

        if (!this.model.src) {
          this.clear();
          return;
        }

        this.setDimensions();
        this.setDominantColor();
      },
    },
  },
  methods: {
    clear() {
      this.model.alt = initialValue.alt;
      this.model.dominant_color = initialValue.dominant_color;
      this.model.height = initialValue.height;
      this.model.src = initialValue.src;
      this.model.title = initialValue.title;
      this.model.width = initialValue.width;
    },
    initWith() {
      return initialValue;
    },
    setDimensions() {
      const img = new Image();
      img.onload = () => {
        this.model.width = img.width;
        this.model.height = img.height;
      };
      img.src = this.model.src;
    },
    async setDominantColor() {
      const colorThief = new ColorThief();
      const corsUrl = `https:${this.model.src.replace(`a.storyblok`, `s3.amazonaws.com/a.storyblok`)}`;
      colorThief.getColorFromUrl(corsUrl, (rgbColor) => {
        this.model.dominant_color = rgb2hex(...rgbColor);
      });
    },
  },
};
</script>
