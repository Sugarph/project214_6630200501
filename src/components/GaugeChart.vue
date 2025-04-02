<template>
    <div class="gauge-wrapper">
      <svg class="gauge" width="300" height="400" viewBox="0 0 220 200">
        <path
          d="M 30 130 A 100 95 0 1 1 190 130"
          fill="none"
          stroke="#333"
          stroke-width="15"
        />
        <path
          class="gauge-progress"
          d="M 30 130 A 100 95 0 1 1 190 130"
          fill="none"
          stroke="#fff"
          stroke-width="15"
          :stroke-dasharray="430"
          :stroke-dashoffset="calcStrokeDashoffset(value, maxValue)"
        />
        <text
          x="110"
          y="80"
          text-anchor="middle"
          fill="#fff"
          font-size="20"
          class="gauge-text"
        >
          <tspan x="110" y="85" class="gauge-number">
            {{ value.toFixed(2) }}
          </tspan>
          <tspan x="110" y="130" class="gauge-label">{{ label }}</tspan>
        </text>
      </svg>
    </div>
  </template>
  
  <script>
  export default {
    name: 'GaugeChart',
    props: {
      value: {
        type: Number,
        required: true
      },
      maxValue: {
        type: Number,
        default: 4
      },
      label: {
        type: String,
        default: 'GPA'
      }
    },
    methods: {
      calcStrokeDashoffset(value, maxValue) {
        const percent = value / maxValue;
        return 430 * (1 - percent);
      }
    }
  }
  </script>
  
  <style scoped>
  .gauge-wrapper {
    flex: 1;
    display: flex;
    justify-content: center;
  }
  
  .gauge-text {
    font-family: Arial, sans-serif;
    font-weight: 700;
  }
  
  .gauge-number {
    font-size: 4rem;
    font-weight: 700;
    letter-spacing: -1px;
  }
  
  .gauge-label {
    font-size: 1.75rem;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  
  .gauge-progress {
    stroke-linecap: butt;
    transition: stroke-dashoffset ease;
  }
  </style>