<template>
  <div class="new-slider">
    <div class="slider">
    <div class="slider__header">
      <button class="slider__button" @click="moveLeft">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M17.5059 6.99927L10.5059 13.9993L17.5059 20.9993" stroke="#1C120D" stroke-width="1.07865" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>

      </button>

      <button class="slider__button" @click="moveRight">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M10.4941 21.0007L17.4941 14.0007L10.4941 7.00073" stroke="#1C120D" stroke-width="1.07865" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>

      </button>
    </div>

    <div ref="sliderRef" class="slider-wrapper">
      <template v-for="(item, index) in items" :key="item.id">
        <transition>
          <div v-show="isDoctorVisible(index)" :class="['item', { active: item.isActive }]" @click="toggleActive(item, index)" >
            <div :class="['text', { hidden: item.isActive }]">
              <span class="text__clinic">{{ item.clinic }}</span>
              <span class="text__name">{{ item.name }}</span>
              <span class="text__position">{{ item.position }}</span>

            </div>
            <img class="img" :src="item.image" alt="" />

            <div class="slider-image__items">
              <button class="slider-image__items-button">
                <svg width="18" height="20" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M17.2245 8.70123L2.48753 0.226436C2.23907 0.0834134 1.9545 0.0053347 1.66321 0.000263788C1.37192 -0.00480712 1.08446 0.0633135 0.830541 0.19759C0.579036 0.329782 0.369526 0.522562 0.223555 0.756107C0.0775834 0.989651 0.000420239 1.25553 0 1.5264V18.4741C0.00189507 18.8804 0.175348 19.2694 0.482229 19.5555C0.78911
                  19.8416 1.2043 20.0015 1.63653 20C1.93822 19.9999 2.23405 19.9217 2.49162 19.774L17.2245 11.2992C17.4613 11.1636 17.6571 10.9729 17.7929 10.7456C17.9287 10.5182 18 10.2619 18 10.0012C18 9.74048 17.9287 9.48415 17.7929 9.25683C17.6571 9.02951 17.4613 8.83884
                   17.2245 8.70315V8.70123ZM1.63653 18.4558V1.5389L16.348 10.0002L1.63653 18.4558Z" fill="#1C120D"/>
                </svg>
              </button>
              <div class="slider-image__items-time">
                {{ item.time }}
              </div>
            </div>
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
,    time: '1:50'
  },
  {
    id: 2,
    name: 'Кустова Наталья Владимировна',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev2.png',
    isActive: false,
    time: '1:50'
  },
  {
    id: 3,
    name: 'Архипенко Анастасия Станиславовна',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev3.png',
    isActive: false,
    time: '1:50'
  },
  {
    id: 4,
    name: 'Архипенко Анастасия Станиславовна',
    position: 'Заведующий отделением пластической хирургии',
    clinic: 'Vip Clinic',
    image: '/images/rev4.png',
    isActive: false,
    time: '1:50'
  },
  {
    id: 5,
    name: 'Доктор #5',
    position: 'Должность четвертого доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev2.png',
    isActive: false,
    time: '1:50'
  },
  {
    id: 6,
    name: 'Доктор #5',
    position: 'Должность четвертого доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev3.png',
    isActive: false,
    time: '1:50'
  },
  {
    id: 7,
    name: 'Доктор #5',
    position: 'Должность четвертого доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev1.png',
    isActive: false,
    time: '1:50'
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
  transition: all 20s cubic-bezier(1, 0.3, 0.3, 1);
}

.v-enter-from {
  opacity: 0;
  transform: translateX(50px);
}
.v-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}

@font-face {
  src: local('TT Firs Text'), url('TTFirs-Regular.woff2') format('woff2');
  font-family: 'TT Firs Text';
  font-weight: 400;
}

.new-slider {
  max-width: fit-content;
}


.slider {
  width: 1839px;
  height: 796px;
  flex-direction: column;
  font-family: 'TT Firs Text', sans-serif;
  aspect-ratio: 1.5 / 1;
  overflow: hidden;
  display: none;

  @media screen and (min-width: 768px) {
    display: block;
  }

  &__header {
    height: fit-content;
    display: flex;
    justify-content: flex-end;
    margin-bottom: 40px;
  }

  &__button {
    width: 64px ;
    height: 64px ;
    display: flex ;
    justify-content: center ;
    align-items: center ;
    background-color: #fff;
    border: 1px solid #fff ;
    border-radius: 12px;
    cursor: pointer;
  }
}

.slider-image__items {
  width: 100%;
  height: 0;
  max-width: 565px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  position: absolute;
  right: 16px;
  bottom: 16px;
  z-index: 100;
  overflow: hidden;
  transition: height 1.5s ease;
  transition-delay: 0.8s;

  &-button {
    width: 80px;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #fff;
    border: 1px solid #fff ;
    border-radius: 12px;
    cursor: pointer;

    svg {
      width: 27px;
      height: 32px;
      padding-left: 5px;
    }
  }

  &-time {
    font-weight: 700;
    font-size: 30px;
    line-height: 35px;
  }
}

.slider-wrapper {
  display: flex;
  height: 692px;
  width: 100%;
  overflow: visible;
}

.item {
  width: 100%;
  height: 100%;
  max-width: 216px;
  position: relative;
  display: flex;
  border-radius: 16px;
  transition: all 0.9s cubic-bezier(.17,.3,.71,.64);
  cursor: pointer;
  overflow: hidden;
  background-color: #fff;

  &:not(:last-child){
    margin-right: 15px;
  }
}

.img {
  right: 0;
  width: 100%;
  max-width: 216px;
  height: 100%;
  position: absolute;
  object-fit: cover;
  transition: all 0.9s cubic-bezier(.17,.3,.71,.64);
  z-index: 1;
}

.text {
  left: 0;
  width: 100%;
  max-width: 216px;
  height: 100%;
  position: absolute;
  display: flex;
  flex-direction: column;
  background: #fff;
  transition: all 0.9s cubic-bezier(.17,.3,.71,.64);
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
  max-width: 1143px;
  z-index: 10;

  .slider-image__items {
    height: 80px;
  }
}

.item.active .img {
  right: 0;
  max-width: 597px;
}

.item.active .text {
  max-width: 546px;
}

.slider-mobile {
  display: flex;
  flex-direction: column;
  row-gap: 8px;

  @media screen and (min-width: 768px) {
    display: none !important;
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
  font-weight: 450;
  line-height: 24px;
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
  margin-top: 12px;
}
</style>
