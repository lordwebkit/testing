<template>
  <swiper
    class="stories-menu-slider"
    :slides-per-view="swiperOptions.slidesPerView"
    v-if="stories.realStories.length"
  >
    <swiper-slide
      class="stories-menu-slider__item"
      v-for="(story, index) in stories.realStories"
      :key="story.id"
      :style="{ backgroundColor: story.bg }"
      @click="openStory(index)"
    >
      <div class="stories-menu-slider__item-preview">
        <img
          class="stories-menu-slider__item-image"
          :src="`https://emi-shop.ru${story.photo}`"
          alt=""
        />
      </div>
      <div class="stories-menu-slider__item-title">
        {{ story.name }}
      </div>
    </swiper-slide>
  </swiper>
</template>

<script setup>
import { ref } from "vue";
import { useStoriesStore } from "@/stores/stories";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";

const stories = useStoriesStore();

const swiperOptions = ref({
  slidesPerView: "auto",
});

const openStory = (index) => {
  stories.storyIndex = index;
  stories.isStoriesActive = true;
};

stories.fetchRealStories();
</script>

<style lang="scss" scoped>
.stories-menu-slider {
  overflow: visible;

  &__item {
    padding: 0.5rem;
    width: 25rem;
    height: 25rem;
    border-radius: 0.75rem;
    cursor: pointer;

    @include r($md) {
      width: 35rem;
      height: 35rem;
    }

    @include r($sm) {
      width: 40rem;
      height: 40rem;
    }

    &:not(:last-child) {
      margin-right: 2rem;
    }

    &-image {
      width: 100%;
    }
    &-title {
      @include text20;

      @include r($sm) {
        font-size: 16px;
      }
    }
  }
}
</style>
