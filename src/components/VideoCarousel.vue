<template>
  <div class="video-holder">
    <swiper :options="swiperOption" @slideChange="handleSlideChange">
      <swiper-slide v-for="video in videos" :key="video.id">
        <single-video :video="video" :ref="`video-${video.id}`"></single-video>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
// eslint-disable-next-line
import 'swiper/dist/css/swiper.css';
import axios from 'axios';
import { swiper, swiperSlide } from 'vue-awesome-swiper';
import SingleVideo from './SingleVideo.vue';

export default {
  name: 'VideoCarousel',
  components: {
    SingleVideo,
    swiper,
    swiperSlide,
  },
  data() {
    return {
      videos: [],
      swiperOption: {
        effect: 'coverflow',
        grabCursor: true,
        centeredSlides: true,
        slidesPerView: 3,
        initialSlide: 1,
        coverflowEffect: {
          rotate: 0,
          stretch: 20,
          depth: 0,
          modifier: 1,
          slideShadows: false,
        },
        breakpoints: {
          480: {
            slidesPerView: 1,
            coverflowEffect: {
              stretch: 0,
            },
          },
        },
        pagination: {
          el: '.swiper-pagination',
        },
      },
    };
  },
  created() {
    this.getVideoSources();
  },
  methods: {
    async getVideoSources() {
      const response = await axios.get('/videos.json');
      if (response.status === 200) {
        this.videos = response.data;
      }
    },
    handleSlideChange() {
      Object.keys(this.$refs).forEach((player) => {
        this.$refs[player][0].stop();
      });
    },
  },
};
</script>

<style  lang="scss">
.swiper-inner {
  width: 100%;
}
.swiper-container {
  padding: 20px 0;
}
.swiper-slide {
  background-position: center;
  background-size: cover;
  width: 250px;
  .single-video {
    transform: scale(0.85);
    .placeholder {
      opacity: 0.6;
    }
  }
}
.swiper-slide-active {
  .single-video {
    transform: scale(1);
    background-color: transparent;
    .placeholder {
      opacity: 1;
    }
    .play-btn {
      display: block;
    }
  }
}
</style>
