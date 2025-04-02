<template>
    <div class="add-year-card" @click="handleClick">
      <div class="add-icon">+</div>
      <p>Add Year</p>
    </div>
  </template>
  
  <script>
  import { EventBus } from "@/event-bus.js";
  
  export default {
    name: "AddYearCard",
    methods: {
      handleClick() {
        EventBus.emit("year:add");
      }
    }
  };
  </script>
  
  <style scoped>
  .add-year-card {
    background: rgba(25, 25, 25, 0.4);
    border: 2px dashed rgba(147, 51, 234, 0.4);
    border-radius: 16px;
    padding: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
    min-height: 120px;
    margin-top: 2rem;
  }
  
  .add-year-card:hover {
    background: rgba(25, 25, 25, 0.6);
    border-color: rgba(147, 51, 234, 0.7);
    transform: translateY(-5px);
  }
  
  .add-icon {
    font-size: 2.5rem;
    color: rgba(147, 51, 234, 0.7);
    line-height: 1;
    font-weight: 300;
    margin-bottom: 0.5rem;
  }
  
  .add-year-card p {
    margin: 0;
    color: #ccc;
    font-size: 1.1rem;
  }
  
  .add-year-card:hover p {
    color: #fff;
  }
  </style>