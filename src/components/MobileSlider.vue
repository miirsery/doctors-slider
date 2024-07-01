<template>
    <div class="slider-mobile">
    <div v-for="(item, index) in props.data" :key="item.id" class="card">
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
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps(['data'])
</script>

<style scoped lang="scss">
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
</style>