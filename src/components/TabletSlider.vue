<template>
  <swiper class="tablet-slider" :slides-per-view="1.1" :space-between="8">
    <swiper-slide v-for="item in props.data" :key="item.id" class="slider">
      <div class="slider__content">
        <span class="slider__content-clinic">{{ item.clinic }}</span>
        <div class="slider__content-name">{{ item.name }}</div>
        <p class="slider__content-title">{{ item.position }}</p>
      </div>
      <div class="slider__image">
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
@font-face {
  src: local('TT Firs Text'), url('TTFirs-Regular.woff2') format('woff2');
  font-family: 'TT Firs Text';
  font-weight: 400;
}

.tablet-slider {
  font-family: 'TT Firs Text', sans-serif;
  position: relative;
  width: 100%;
  height: 100%;
  max-width: 720px;
  max-height: 435px;
  display: none;



  @media screen and (min-width: 768px) and (max-width: 1439px) {
    display: block !important;
  }


  @media screen and (max-width: 767px) {
    display: none !important;
  }

  .slider {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    border-radius: 10px;
    overflow: hidden;

    &__content {
      width: 100%;
      max-width: 306px;
      display: flex;
      flex-direction: column;
      padding: 20px;
      background-color: #fff;


      &-clinic {
        margin: 0;
        font-size: 16px;
        line-height: 104%;
        letter-spacing: -0.03em;
        color: #1c120d;
        text-align: left;
      }

      &-name {
        margin: 16px 0 12px;
        font-size: 40px;
        line-height: 110%;
        font-weight: 700;
        letter-spacing: -0.03em;
      }

      &-position {
        margin: 0;
        font-size: 16px;
        line-height: 104%;
        letter-spacing: 0.05em;
        color: #96918b;
      }
    }

    &__image {
      img {
        width: 100%;
        height: 100%;
        max-width: 346px;
        max-height: 435px;
        object-fit: cover;
        border-radius: 10px;
        overflow: hidden;
      }
    }
  }
}

.swiper-wrapper {
  border-radius: 10px;
  overflow: hidden;
}
</style>
