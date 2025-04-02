<template>
  <div class="background-rotator">
    <div
      v-for="(image, index) in images"
      :key="index"
      class="background-image"
      :class="{ active: index === currentIndex }"
      :style="{ 
        backgroundImage: `url(${image})`, 
        zIndex: index === currentIndex ? 1 : 0,
        transition: `opacity ${transitionDuration}ms ease-in-out`
      }"
    ></div>
  </div>
</template>

  <script>
  export default {
    name: 'BackgroundRotator',
    props: {
      images: { type: Array, required: true },
      interval: { type: Number, default: 4000 },
      transitionDuration: { type: Number, default: 1500 }
    },
    data() {
      return { currentIndex: 0 };
    },
    mounted() {
      if (this.images.length > 1) {
        this.rotationInterval = setInterval(() => {
          this.currentIndex = (this.currentIndex + 1) % this.images.length;
        }, this.interval);
      }
    },
    beforeDestroy() {
      clearInterval(this.rotationInterval);
    }
  };
  </script>
  
  <style scoped>
  .background-rotator {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }
  
  .background-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    opacity: 0;
  }
  
  .background-image.active {
    opacity: 0.7;
  }
  </style>