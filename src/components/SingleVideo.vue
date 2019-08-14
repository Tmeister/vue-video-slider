<template>
  <div class="single-video">
    <img class="placeholder" :src="video.placeholder" :alt="video.title" />
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
};
</script>

<style lang="scss" scope>
.single-video {
  max-width: 250px;
  .placeholder {
    max-width: 100%;
  }
}
</style>
