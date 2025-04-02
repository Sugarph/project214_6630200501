<template>
    <div class="side-content" :class="position">
      <h3>{{ value }}</h3>
      <h3>{{ label }}</h3>
    </div>
  </template>
  
  <script>
  export default {
    name: 'StatNumber',
    props: {
      value: {
        type: Number,
        required: true
      },
      label: {
        type: String,
        required: true
      },
      position: {
        type: String,
        default: 'left-content',
        validator: value => ['left-content', 'right-content'].includes(value)
      }
    }
  }
  </script>
  
  <style scoped>
  .side-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .side-content h3:first-child {
    font-weight: 700;
    font-size: 4.5rem;
    margin: 0;
    line-height: 1;
    letter-spacing: -2px;
  }
  
  .side-content h3:last-child {
    font-weight: 500;
    font-size: 1.75rem;
    margin-top: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  
  .left-content {
    justify-self: start;
    margin-left: 4rem;
  }
  
  .right-content {
    justify-self: end;
    margin-right: 4rem;
  }
  </style>