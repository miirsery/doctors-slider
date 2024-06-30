<template>
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
      <div v-for="(item, index) in items" :key="item.id" :class="['item', { active: item.isActive }]" @click="toggleActive(item, index)">
        <div :class="['text', { hidden: item.isActive }]">
          <span class="text__clinic">{{ item.clinic }}</span>
          <span class="text__name">{{ item.name }}</span>
          <span class="text__position">{{ item.position }}</span>
        </div>
        <img class="img" :src="item.image" alt="" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from 'vue'

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
    name: 'Доктор #2',
    position: 'Должность второго доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev2.png',
    isActive: false
  },
  {
    id: 3,
    name: 'Доктор #3',
    position: 'Должность третьего доктора',
    clinic: 'Vip Clinic',
    image: '/images/rev3.png',
    isActive: false
  },
  {
    id: 4,
    name: 'Доктор #4',
    position: 'Должность четвертого доктора',
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
])

const sliderRef = ref()
const counter = ref()
const currentIndex = ref(0)

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

  clickedItem.isActive = !clickedItem.isActive

  if (index > 2) {
    counter.value++

    sliderRef.value.style.transform = `translateX(-216px)`
  }
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

onMounted(() => {
  window.addEventListener('click', clickOutsideHandler)
})

onUnmounted(() => {
  window.removeEventListener('click', clickOutsideHandler)
})
</script>


<style lang="scss" scoped>
@font-face {
  src: local('TT Firs Text'), url('../TTFirs-Regular.woff2') format('woff2');
  font-family: 'TT Firs Text';
  font-weight: 400;
}

.slider {
  width: 1440px;
  height: 692px;
  display: flex;
  flex-direction: column;
  font-family: 'TT Firs Text', sans-serif;
  aspect-ratio: 1.5 / 1;
  overflow: hidden;
}

.slider-wrapper {
  display: flex;
  height: 100%;
  width: 100%;
  overflow: hidden;
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
</style>
