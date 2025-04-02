<template>
    <component 
      :is="tag" 
      :to="to" 
      :href="href" 
      :target="target" 
      class="animated-btn"
    >
      <i v-for="index in 10" :key="index"></i>
      <span><slot></slot></span>
    </component>
  </template>
  
  <script>
  export default {
    name: 'AnimatedButton',
    props: {
      tag: {
        type: String,
        default: 'button',
        validator: value => ['button', 'a', 'router-link'].includes(value)
      },
      to: {
        type: String,
        default: ''
      },
      href: {
        type: String,
        default: ''
      },
      target: {
        type: String,
        default: ''
      }
    }
  }
  </script>
  
  <style scoped>
  .animated-btn {
    --c: cubic-bezier(1, .49, .16, .96);
    position: relative;
    display: inline-block;
    color: #fff;
    text-decoration: none;
    text-transform: uppercase;
    border: 2px solid #fff;
    padding: 1.25em 3em;
    margin-top: 1em;
    overflow: hidden;
    z-index: 1;
    background: rgba(0, 0, 0, 0);
    -webkit-tap-highlight-color: transparent;
    user-select: none;
  }
  
  .animated-btn span {
    position: relative;
    font-weight: 600;
    letter-spacing: 2px;
    z-index: 3;
    mix-blend-mode: difference;
    transition: color 0.1s var(--c);
  }
  
  .animated-btn i {
    position: absolute;
    top: 0;
    width: 100.5%;
    height: 10%;
    background: #fff;
    z-index: 2;
    transform: scaleX(0);
    transform-origin: left;
    left: 0;
    transition: transform 0.16s var(--c), transform-origin 0s;
  }
  
  .animated-btn i:nth-child(1) { top: 0%; transition-delay: .02s; }
  .animated-btn i:nth-child(2) { top: 10%; transition-delay: .04s; }
  .animated-btn i:nth-child(3) { top: 20%; transition-delay: .06s; }
  .animated-btn i:nth-child(4) { top: 30%; transition-delay: .08s; }
  .animated-btn i:nth-child(5) { top: 40%; transition-delay: .10s; }
  .animated-btn i:nth-child(6) { top: 50%; transition-delay: .12s; }
  .animated-btn i:nth-child(7) { top: 60%; transition-delay: .14s; }
  .animated-btn i:nth-child(8) { top: 70%; transition-delay: .16s; }
  .animated-btn i:nth-child(9) { top: 80%; transition-delay: .18s; }
  .animated-btn i:nth-child(10) { top: 90%; transition-delay: .20s; }
  
  .animated-btn:hover i {
    transform: scaleX(1);
    transform-origin: left;
  }
  
  .animated-btn:not(:hover) i {
    transform: scaleX(0);
    transform-origin: right;
  }
  </style>