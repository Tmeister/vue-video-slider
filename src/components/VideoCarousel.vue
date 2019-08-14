<template>
  <div class="video-holder">
    <single-video v-for="video in videos" :key="video.id" :video="video"></single-video>
  </div>
</template>

<script>
import axios from 'axios';
import SingleVideo from './SingleVideo.vue';

export default {
  name: 'VideoCarousel',
  components: {
    SingleVideo,
  },
  data() {
    return {
      videos: [],
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
  },
};
</script>

<style scoped lang="scss">
</style>
