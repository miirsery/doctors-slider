<template>
  <div class="doctors-swiper__wrapper">
    <swiper
      ref="swiperRef"
      :modules="modules"
      slides-per-view="auto"
      class="doctors-swiper"
      centered-slides
      :effect="'coverflow'"
      @swiper="doctorsSwiper"
      @slide-change="onSlideChange"
    >
      <swiper-slide
        v-for="card in doctorsSwiperDate"
        :key="card.id"
        v-slot="{ isActive }"
        class="doctors-swiper__slide"
        @click="setActiveSlide(card.id)"
      >
        <transition name="content-animation">
          <div v-if="isActive" class="doctors-swiper__slide-content">
            <span class="doctors-swiper__slide-content--clinic">{{ card.clinic }}</span>
            <div class="doctors-swiper__slide-content--name"> {{ card.name }}</div>
            <p class="doctors-swiper__slide-content--position"> {{ card.position }}</p>
          </div>
        </transition>

        <img class="doctors-swiper__slide-video" :src="card.image" />
      </swiper-slide>
    </swiper>
  </div>
</template>

<script lang="ts" setup>
import { Navigation, Pagination, Scrollbar, A11y } from 'swiper/modules'
import { Swiper, SwiperSlide } from 'swiper/vue'
import 'swiper/css'
import 'swiper/css/navigation'
import 'swiper/css/pagination'
import 'swiper/css/scrollbar'
import { ref } from 'vue'
import {doctorsSwiperDate} from "../mocks";

const modules = [Navigation, Pagination, Scrollbar, A11y]

const swiperRef = ref()

const doctorsSwiper = (swiper: any) => {

  swiperRef.value = swiper
}

const onSlideChange = () => {
  console.log('slide change')
}

const setActiveSlide = (index: number) => {
  swiperRef.value.slideToLoop(index, 500, true)
}
</script>

<style lang="scss" scoped>
.swiper {
  width: 100%;
}

.doctors-swiper__wrapper {
  width: 100%;
  max-width: 1839px;

  :deep(.swiper-wrapper) {
    transform: none !important;
  }
}

.doctors-swiper {
  width: 100%;
  height: 692px;
  display: flex;
  font-family: 'TT Firs Text', sans-serif;

  &__slide {
    width: 216px;
    display: flex;
    flex: 0 0 auto;
    justify-content: space-between;
    border-radius: 16px;
    background-color: #fff;
    transition: width 1s ease-in-out, max-width 1s ease-in-out;
    margin-right: 15px;
    overflow: hidden;

    &-content {
      max-width: 546px;
      display: none;
      flex-direction: column;
      transition: max-width 1s ease-in-out, padding 1s ease-in-out;
      padding: 32px;
      gap: 17px;

      &--clinic {
        font-size: 20px;
        line-height: 120%;
        letter-spacing: -0.02em;
        color: #96918b;
      }

      &--name {
        font-size: 64px;
        line-height: 104%;
        letter-spacing: -0.03em;
        color: #1c120d;
      }

      &--position {
        font-size: 24px;
        line-height: 120%;
        letter-spacing: 0.05em;
        color: #96918b;
      }
    }

    .doctors-swiper__slide-video {
      width: 100%;
      height: 100%;
      max-width: 216px;
      border-radius: 0 16px 16px 0;
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;
      object-fit: cover;
      transition: max-width 1s ease-in-out;
    }

    &.swiper-slide-active {
      width: 1143px;

      .doctors-swiper__slide-content {
        display: flex;
      }

      .doctors-swiper__slide-video {
        max-width: 597px;
      }
    }
  }

  @font-face {
    src: local('TT Firs Text'), url('../TTFirs-Regular.woff2') format('woff2');
    font-family: 'TT Firs Text';
    font-weight: 400;
  }
}

.content-animation-enter-active,
.content-animation-leave-active {
  transition: max-width 1s ease-in-out, padding 1s ease-in-out;
  overflow: hidden;
}

.content-animation-enter-from,
.content-animation-leave-to {
  max-width: 0;
  padding: 0;
}

.content-animation-enter-to,
.content-animation-leave-from {
  max-width: 546px;
  padding: 32px;
}
</style>
