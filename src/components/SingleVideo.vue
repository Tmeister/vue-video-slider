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

<style lang="scss">
.single-video {
  max-width: 250px;
  border-radius: 5px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
  background-color: black;
  display: flex;
  margin-bottom: 20px;
  .placeholder {
    max-width: 100%;
    border-radius: 5px;
    opacity: 0.6;
  }
}
</style>
