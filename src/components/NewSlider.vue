<template>
  <div class="new-slider">
    <div class="slider">
      <div class="slider__header">
        <button class="button" @click="moveLeft">
          Left
        </button>

        <button class="button" @click="moveRight">
          Right
        </button>
      </div>

      <div ref="sliderRef" class="slider-wrapper">
        <template v-for="(item, index) in items" :key="item.id">
          <transition>
            <div v-show="isDoctorVisible(index)" :class="['item', { active: item.isActive }]" @click="toggleActive(item, index)">
              <div :class="['text', { hidden: item.isActive }]">
                <span class="text__clinic">{{ item.clinic }}</span>
                <span class="text__name">{{ item.name }}</span>
                <span class="text__position">{{ item.position }}</span>
              </div>
              <img class="img" :src="item.image" alt="" />
            </div>
          </transition>
        </template>
      </div>
    </div>

    <div class="slider-mobile">
      <div v-for="(item, index) in items" :key="item.id" class="card">
        <div class="card-header">
          <div class="card-image" :style="{ backgroundImage: 'url(' + item.image + ')' }"></div>
        </div>
        <div class="card-body">
          <h4 class="clinic-name">{{ item.clinic }}</h4>
          <h3 class="doctor-name">{{ item.name }}</h3>
          <p class="doctor-title">{{ item.position }}</p>
        </div>

        <div class="card-footer">
          <button class="play-button">
            <div class="play-button__image">
              <img src="/play.svg" />
            </div>

            Смотреть отзыв
          </button>

          <span class="video-duration">1:50</span>
        </div>
      </div>
    </div>

    <button class="show-more">
      Показать еще
    </button>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted, computed, watch } from 'vue'

const items = ref([
  {
    id: 1,
    name: 'Круглик Сергей Викторович',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev1.png',
    isActive: true
  },
  {
    id: 2,
    name: 'Кустова Наталья Владимировна',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev2.png',
    isActive: false
  },
  {
    id: 3,
    name: 'Архипенко Анастасия Станиславовна',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev3.png',
    isActive: false
  },
  {
    id: 4,
    name: 'Архипенко Анастасия Станиславовна',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev4.png',
    isActive: false
  },
  {
    id: 5,
    name: 'Доктор #5',
    position: 'Должность четвертого доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev4.png',
    isActive: false
  },
  {
    id: 6,
    name: 'Доктор #5',
    position: 'Должность четвертого доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev4.png',
    isActive: false
  },
  {
    id: 7,
    name: 'Доктор #5',
    position: 'Должность четвертого доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev4.png',
    isActive: false
  },
])

const sliderRef = ref()
const currentIndex = ref(0)

const isDoctorVisible = (index) => {
  if (currentIndex.value < 2){
    return index < 4
  }

  if (currentIndex.value > index){
    return currentIndex.value - index < 3
  }
  if (currentIndex.value < index){
    return index - currentIndex.value === 1
  }
  return true
}

const clearActiveImage = () => {
  items.value.forEach((item) => {
    item.isActive = false
  })
}

const setActiveImage = (index) => {
  clearActiveImage()
  items.value[index].isActive = true
}

const toggleActive = (clickedItem, index) => {
  clearActiveImage()
  currentIndex.value = index

  clickedItem.isActive = !clickedItem.isActive
}

const moveLeft = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
  } else {
    currentIndex.value = items.value.length - 1
  }
  setActiveImage(currentIndex.value)
}

const moveRight = () => {
  if (currentIndex.value < items.value.length - 1) {
    currentIndex.value++
  } else {
    currentIndex.value = 0
  }
  setActiveImage(currentIndex.value)
}

const clickOutsideHandler = (event) => {
  const sliderElement = document.querySelector('.slider')
  if (sliderElement && !sliderElement.contains(event.target)) {
    clearActiveImage()
  }
}

onUnmounted(() => {
  window.removeEventListener('click', clickOutsideHandler)
})
</script>

<style lang="scss" scoped>
.v-enter-active,
.v-leave-active {
  transition: all 10s cubic-bezier(1, 0.5, 0.8, 1);
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}

@font-face {
  src: local('TT Firs Text'), url('../TTFirs-Regular.woff2') format('woff2');
  font-family: 'TT Firs Text';
  font-weight: 400;
}

.slider {
  width: 1500px;
  height: 692px;
  display: flex;
  flex-direction: column;
  font-family: 'TT Firs Text', sans-serif;
  aspect-ratio: 1.5 / 1;
  overflow: hidden;
  display: block;

  @media screen and (max-width: 768px) {
    display: none;
  }
}

.slider-wrapper {
  display: flex;
  height: 100%;
  width: 100%;
  overflow: visible;
}

.item {
  width: calc(100% / 5);
  height: 100%;
  position: relative;
  display: flex;
  border-radius: 16px;
  transition: all 0.4s cubic-bezier(0.32, 0, 0.67, 0);
  cursor: pointer;
  overflow: hidden;
  background-color: #fff;

  &:not(:last-child) {
    margin-right: 15px;
  }
}

.img {
  left: 0;
  width: 100%;
  height: 100%;
  position: absolute;
  object-fit: cover;
  transition: all 0.4s cubic-bezier(0.32, 0, 0.67, 0);
  z-index: 1;
}

.text {
  left: 0;
  width: 15%;
  height: 100%;
  position: absolute;
  display: flex;
  flex-direction: column;
  background: #fff;
  transition: all 0.4s cubic-bezier(0.32, 0, 0.67, 0);
  padding: 32px;
  z-index: 0;
  gap: 17px;

  &__clinic {
    font-size: 20px;
    line-height: 120%;
    letter-spacing: -0.02em;
    color: #96918b;
  }

  &__name {
    font-size: 64px;
    line-height: 104%;
    letter-spacing: -0.03em;
    color: #1c120d;
    text-align: left;
  }

  &__position {
    font-size: 24px;
    line-height: 120%;
    letter-spacing: 0.05em;
    color: #96918b;
  }
}

.item.active {
  width: 200%;
  z-index: 10;
}

.item.active .img {
  left: 40%;
  width: 60%;
}

.item.active .text {
  width: 32%;
}

.slider-mobile {
  display: flex;
  flex-direction: column;
  row-gap: 8px;
  display: none;

  @media screen and (max-width: 768px) {
    display: block !important;
  }
}

.card {
  width: 100%;
  border-radius: 10px;
  overflow: hidden;
  background: #fff;
  height: 466px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  font-family: 'TT Firs Text', sans-serif;
}

.card-header {
  position: relative;
}

.card-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  background-position: 0 0px;
  background-repeat: no-repeat;
  background-size: 100%;
  border-radius: 12px;
}

.card-body {
  padding: 16px;
  text-align: left;
  flex-grow: 1;
}

.doctor-name {
  color: #1C120D;
  margin-top: 8px;
  font-size: 24px;
  margin: 0;
  font-weight: 450;
  line-height: 24px;
  margin-top: 8px;
  max-width: 217px;
}

.doctor-title,
.clinic-name {
  font-size: 14px;
  color: #96918B;
  margin: 0;
  max-width: 217px;
}

.doctor-title {
  margin-top: 4px;
}

.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  border: 1px solid #BBBBBB66;
  border-radius: 12px;
  margin: 0 12px 12px 12px;
  font-size: 14px;
  line-height: 14px;
  color: #1C120D;
}

.play-button {
  display: flex;
  align-items: center;
  background: none;
  color: #1C120D;
  font-size: 14px;
  cursor: pointer;
  border: none;
  padding: 0;

  &__image {
    background-color: #F1EFE9;
    width: 50px;
    height: 50px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 12px;
  }
}

.show-more {
  width: 100%;
  padding: 24px 12px;
  color: #1C120D;
  font-size: 14px;
  line-height: 16.8px;
  text-align: center;
  border-radius: 12px;
  background-color: #fff;
  border-radius: 12px;
  margin-top: 12px;
  display: none;
  
  @media screen and (max-width: 768px) {
    display: block !important;
  }
}
</style>
