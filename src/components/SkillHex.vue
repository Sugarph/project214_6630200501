<template>
  <div class="skill-hex" @click="toggleDetails" :style="hexStyle">
    <div class="hex-container">
      <div class="hex-inner">
        <img :src="icon" :alt="name" class="skill-icon" :style="{ transform: `scale(${size})` }">
      </div>
    </div>
    <transition name="fade">
      <span v-if="showDetails" class="skill-name" :style="nameStyle">
        {{ name }}
      </span>
    </transition>
  </div>
</template>

<script>
export default {
  name: "SkillHex",
  props: {
    name: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
      required: true,
    },
    color: {
      type: String,
      default: "#9333EA",
    },
    size: {
      type: Number,
      default: 1,
    },
  },
  data() {
    return {
      showDetails: false,
    };
  },
  computed: {
    hexStyle() {
      return {
        "--hex-color": this.color,
        "--hex-shadow": `${this.color}80`, // 50% opacity
      };
    },
    nameStyle() {
      return {
        background: `${this.color}E6`, // 90% opacity
      };
    },
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },
  },
};
</script>

<style scoped>
.skill-hex {
  position: relative;
  width: 180px;
  filter: drop-shadow(0 0 0 var(--hex-shadow));
  transition: filter 0.3s ease;
  cursor: pointer;
}

.skill-hex:hover {
  filter: drop-shadow(0 0 20px var(--hex-shadow));
  z-index: 10;
}

.hex-container {
  width: 180px;
  height: 208px;
  position: relative;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
}

.hex-inner {
  position: absolute;
  inset: 4px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: rgb(25, 25, 25);
  z-index: 1;
}

.hex-container::before {
  content: "";
  position: absolute;
  width: 200%;
  height: 200%;
  top: -50%;
  left: -50%;
  background: linear-gradient(
    45deg,
    transparent 30%,
    var(--hex-color) 40%,
    var(--hex-color) 60%,
    transparent 70%
  );
  opacity: 0.5;
  transform: rotate(0deg);
  transition: all 0.5s ease;
}

.hex-container:hover {
  transform: translateY(-5px);
}

.hex-container:hover::before {
  transform: rotate(180deg);
}

.hex-container img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  padding: 2rem;
  transition: all 0.3s ease;
  filter: brightness(0.9);
  position: relative;
  z-index: 2;
}

.hex-container:hover img {
  filter: brightness(1.2);
  transform: scale(1.1);
}

.skill-name {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  color: #fff;
  font-size: 1rem;
  font-weight: 500;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  white-space: nowrap;
  z-index: 10;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s, transform 0.3s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(-10px);
}
</style>
