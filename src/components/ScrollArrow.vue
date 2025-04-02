<template>
    <div 
      class="scroll-arrow" 
      @click="$emit('click')"
      :style="{
        opacity: opacity,
        transform: `translateY(${translateY}px)`
      }"
    >
      <svg width="30px" height="20px">
        <path
          stroke="#ffffff"
          fill="none"
          stroke-width="2px"
          d="M2.000,5.000 L15.000,18.000 L28.000,5.000"
        ></path>
      </svg>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ScrollArrow',
    props: {
      translateY: {
        type: Number,
        default: 0
      },
      opacity: {
        type: Number,
        default: 1
      }
    }
  }
  </script>
  
  <style scoped>
  .scroll-arrow {
    position: absolute;
    left: 50%;
    bottom: 20px;
    transform: translateX(-50%);
    animation: bounce 5s cubic-bezier(0.4, 0, 0.2, 1) infinite;
    cursor: pointer;
    z-index: 10;
  }
  
  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translateY(0) translateX(-50%);
    }
    0%, 20%{
        opacity: 0;
    }
    40% {
      transform: translateY(-10px) translateX(-50%);
      opacity: 1;
    }
    60% {
      transform: translateY(-5px) translateX(-50%);
      opacity: 1;
    }
    100% {
        opacity: 0;
    }
  }
  </style>