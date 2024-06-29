<template>
  <div class="doctors-slider">
    <div class="doctors-slider__navigation">
      <button type="button" @click="prevSlide">Prev</button>
      <button type="button" @click="nextSlide">Next</button>
    </div>

    <div class="doctors-slider__inner">
      <div
          v-for="(item, index) in data"
          :key="item.id"
          :style="{ ...slideStyle, ...(index === currentIndex ? activeSlideStyle : {}) }"
          class="doctor-slide"
          @click="slideClick(index)"
      >
        <img :src="item.image" />
        <div>КАКОЙ-ТО ТЕКСТ</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const data = [
  {
    id: 1,
    image: 'https://img.goodfon.ru/original/2560x1600/c/1c/anime-devushka-melanholiya.jpg',
  },
  {
    id: 2,
    image: 'https://www.digiseller.ru/preview/319113/p1_3387264_15533dde.jpg',
  },
  {
    id: 3,
    image: 'https://www.digiseller.ru/preview/319113/p1_3387264_269a0a38.jpg',
  },
  {
    id: 4,
    image: 'https://img.goodfon.ru/original/2560x1600/c/1c/anime-devushka-melanholiya.jpg',
  },
  {
    id: 5,
    image: 'https://www.digiseller.ru/preview/319113/p1_3387264_15533dde.jpg',
  },
  {
    id: 6,
    image: 'https://www.digiseller.ru/preview/319113/p1_3387264_269a0a38.jpg',
  },
];

const currentIndex = ref(0);
const slidesToShow = 4;

const nextSlide = () => {
  if (currentIndex.value < data.length - slidesToShow) {
    currentIndex.value += 1;
  }
};

const prevSlide = () => {
  if (currentIndex.value > 0) {
    currentIndex.value -= 1;
  }
};

const slideClick = (index) => {
  currentIndex.value = index;
};

const slideStyle = computed(() => ({
  width: `calc(${100 / slidesToShow}% - 16px)`,
  minWidth: `calc(${100 / slidesToShow}% - 16px)`,
  marginRight: '16px',
  transition: 'transform 0.3s ease-in-out',
  transform: `translateX(calc(-${currentIndex.value * (100 / slidesToShow) - 32}%))`,
}));

const activeSlideStyle = computed(() => ({
  transform: `translateX(calc(-${currentIndex.value * (100 / slidesToShow)}%))`,
}));

</script>

<style lang="scss" scoped>
.doctors-slider {
  width: 100%;

  &__inner {
    width: 100%;
    overflow: hidden;
    display: flex;
    position: relative;
  }

  .doctor-slide {
    box-sizing: border-box;
    display: flex;
    align-items: center;
    background-color: #f9f9f9;
    color: #f90;
    font-weight: 600;
    cursor: pointer;
  }

  img {
    width: 150px;
    height: 150px;
    object-fit: cover;
    object-position: 25% 25%;
    display: block;
  }
}
</style>
