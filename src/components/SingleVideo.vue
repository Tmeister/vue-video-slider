<template>
  <div class="single-video">
    <div class="preview" v-if="!isPlaying">
      <img class="placeholder" :src="video.placeholder" :alt="video.title" />
      <span class="title">{{video.title}}</span>
      <svg
        class="play-btn"
        @click="handlePlayVideoClick"
        fill="#ffffff"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        version="1.1"
        x="0px"
        y="0px"
        viewBox="0 0 100 100"
        style="enable-background:new 0 0 100 100;"
        xml:space="preserve"
      >
        <path
          d="M50,1C22.9,1,1,22.9,1,50s21.9,49,49,49s49-21.9,49-49S77.1,1,50,1z
          M50,89.8C28,89.8,10.2,72,10.2,50S28,10.2,50,10.2
          S89.8,28,89.8,50S72,89.8,50,89.8z M37.8,28.6L74.5,50L37.8,71.4V28.6z"
        />
      </svg>
    </div>
    <div class="player" v-if="isPlaying">
      <video width="100%" height="auto" controls autoplay @ended="handleEndVideo">
        <source :src="video.url" type="video/mp4" />Your browser does not support the video tag.
      </video>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SingleVideo',
  props: {
    video: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      isPlaying: false,
    };
  },
  methods: {
    handlePlayVideoClick() {
      this.isPlaying = true;
    },
    handleEndVideo() {
      this.isPlaying = false;
    },
    stop() {
      if (this.isPlaying) {
        this.isPlaying = false;
      }
    },
  },
};
</script>

<style lang="scss">
.single-video {
  width: 250px;
  border-radius: 5px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
  background-color: black;
  margin-bottom: 20px;
  margin: 0 auto;
  position: relative;
  .preview,
  .player {
    display: flex;
  }
  .player {
    video {
      border-radius: 5px;
    }
  }
  .placeholder {
    max-width: 100%;
    border-radius: 5px;
  }
  .play-btn {
    position: absolute;
    width: 76px;
    height: 76px;
    left: 50%;
    margin-left: -38px;
    top: 50%;
    margin-top: -38px;
    display: none;
    cursor: pointer;
  }
  .title {
    position: absolute;
    left: 10px;
    bottom: 10px;
    color: white;
    font-size: 14px;
    text-transform: uppercase;
    text-shadow: 2px 2px rgba(0, 0, 0, 0.2);
  }
}
</style>
