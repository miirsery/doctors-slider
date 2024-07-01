<template>
  <swiper class="tablet-slider">
    <swiper-slide v-for="item in props.data" :key="item.id" class="slider">
      <div class="slider__content">
        <h4 class="slider__content-clinic">{{ item.clinic }}</h4>
        <h3 class="slider__content-name">{{ item.name }}</h3>
        <p class="slider__content-title">{{ item.position }}</p>
      </div>
      <div class="tablet-slider__image">
        <img :src="item.image" />
      </div>
    </swiper-slide>
  </swiper>
</template>

<script setup lang="ts">
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

import { defineProps } from 'vue';

const props = defineProps(['data'])
</script>

<style lang="scss" scoped>
.tablet-slider {
  width: 100%;
  height: 100%;
  max-width: 720px;
  max-height: 435px;
  display: none;
  flex-direction: row;
  row-gap: 8px;



  @media screen and (max-width: 1440px) {
    display: block !important;
  }

  .slider {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    border-radius: 10px;
  }
}
</style>
