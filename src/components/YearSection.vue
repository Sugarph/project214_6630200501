<template>
    <div class="year-section" :class="{ expanded: expanded }">
      <div
        class="year-header"
        :class="{ expanded: expanded }"
        @click="toggleExpansion"
      >
        <div class="gradient-overlay" :style="gradientOverlayStyle"></div>
        <h3>Year {{ year }}</h3>
        <div class="year-stats">
          <span>{{ yearCredits }} Credits</span>
          <span>GPA: <span :style="gpaTextStyle">{{ yearGPA }}</span></span>
        </div>
        <div class="expand-icon" :style="expandIconStyle">
          <svg
            class="icon-container"
            viewBox="0 0 24 24"
            width="24"
            height="24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <line
              class="horizontal-line"
              x1="6"
              y1="12"
              x2="18"
              y2="12"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              :style="{
                transform: expanded ? 'rotate(90deg)' : 'rotate(0deg)',
                opacity: expanded ? 0 : 1,
              }"
            />
            <line
              class="vertical-line"
              x1="12"
              y1="6"
              x2="12"
              y2="18"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              :style="{ transform: expanded ? 'rotate(90deg)' : 'rotate(0deg)' }"
            />
          </svg>
        </div>
      </div>
  
      <transition name="slide">
        <div class="courses-grid" v-if="expanded">
          <course-card
            v-for="course in yearCourses"
            :key="course.id"
            :course="course"
          />
          <add-course-card :year="year" />
        </div>
      </transition>
    </div>
  </template>
  
  <script>
  import CourseCard from "@/components/CourseCard.vue";
  import AddCourseCard from "@/components/AddCourseCard.vue";
  
  export default {
    name: "YearSection",
    components: {
      CourseCard,
      AddCourseCard,
    },
    props: {
      year: {
        type: Number,
        required: true,
      },
      courses: {
        type: Array,
        required: true,
      },
      initialExpanded: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        expanded: this.initialExpanded,
      };
    },
    computed: {
      yearCourses() {
        return this.courses.filter((course) => course.year === this.year);
      },
      yearCredits() {
        return this.yearCourses.reduce((total, course) => {
          return total + Number(course.credits);
        }, 0);
      },
      yearGPA() {
        let totalCredits = 0;
        let totalGradePoints = 0;
  
        const gradePoints = {
          A: 4.0,
          "B+": 3.5,
          B: 3.0,
          "C+": 2.5,
          C: 2.0,
          "D+": 1.5,
          D: 1.0,
          F: 0.0,
        };
  
        this.yearCourses.forEach((course) => {
          totalCredits += Number(course.credits);
          totalGradePoints +=
            Number(course.credits) * (gradePoints[course.grade] || 0);
        });
  
        return totalCredits > 0
          ? (totalGradePoints / totalCredits).toFixed(2)
          : "0.00";
      },
      gpaGradient() {
        const gpa = parseFloat(this.yearGPA);
        const percentage = (gpa / 4.0) * 100;
  
        const red = Math.max(255 - percentage * 2.55, 0);
        const green = Math.min(percentage * 2.55, 255);
        const blue = 0;
  
        return `rgba(${red}, ${green}, ${blue}, 0.3)`;
      },
      gradientOverlayStyle() {
        if (this.yearCourses.length === 0) {
          return {
            background: `linear-gradient(
                45deg,
                transparent 30%,
                rgba(147, 51, 234, 0.3) 40%,
                rgba(147, 51, 234, 0.3) 60%,
                transparent 70%
              )`,
          };
        }
  
        return {
          background: `linear-gradient(
              45deg,
              transparent 30%,
              ${this.gpaGradient} 40%,
              ${this.gpaGradient} 60%,
              transparent 70%
            )`,
        };
      },
      gpaTextStyle() {
        if (this.yearCourses.length === 0) return {};
  
        const gpa = parseFloat(this.yearGPA);
        const percentage = (gpa / 4.0) * 100;
  
        const red = Math.max(255 - percentage * 2.55, 0);
        const green = Math.min(percentage * 2.55, 255);
        const blue = 0;
  
        return { color: `rgb(${red}, ${green}, ${blue})`, fontWeight: "600" };
      },
      expandIconStyle() {
        if (this.yearCourses.length === 0) {
          return { background: "rgba(147, 51, 234, 0.3)" };
        }
  
        return { background: this.gpaGradient };
      },
    },
    methods: {
      toggleExpansion() {
        this.expanded = !this.expanded;
      },
    },
  };
  </script>
  
  <style scoped>
  .year-section {
    background: rgba(25, 25, 25, 0.6);
    border-radius: 16px;
    overflow: hidden;
    transition: all 0.3s ease; /* Smooth transition for all animated properties */
    filter: drop-shadow(0 0 0 rgba(0, 0, 0, 0.5));
    margin-bottom: 3rem;
    border-left: 5px solid transparent;
    max-height: 80px; /* Collapsed height (approx height of year-header) */
  }
  
  .year-section.expanded {
    max-height: 1000px; /* Large enough to fit content; adjust as needed */
  }
  
  .year-section:hover {
    filter: drop-shadow(0 0 10px rgba(0, 0, 0, 0.5));
  }
  
  .year-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 2rem;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease;
    background: linear-gradient(
      to right,
      rgba(25, 25, 25, 1),
      rgba(25, 25, 25, 0.9)
    );
  }
  
  .gradient-overlay {
    content: "";
    position: absolute;
    inset: 0;
    opacity: 0.3;
    transform: translateX(-100%);
    transition: all 0.5s ease;
    z-index: 0;
  }
  
  .year-header:hover .gradient-overlay,
  .year-header.expanded .gradient-overlay {
    transform: translateX(0);
  }
  
  .year-header h3 {
    font-size: 1.8rem;
    margin: 0;
    font-weight: 600;
    color: #fff;
    position: relative;
    z-index: 1;
  }
  
  .year-stats {
    display: flex;
    gap: 2rem;
    color: rgb(170, 170, 170);
    font-size: 1.1rem;
    position: relative;
    z-index: 1;
  }
  
  .expand-icon {
    width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    color: white;
    position: relative;
    z-index: 1;
    transition: all 0.3s ease;
  }
  
  .year-header:hover .expand-icon,
  .year-header.expanded .expand-icon {
    opacity: 0.9;
    transform: scale(1.1);
  }
  
  .icon-container {
    display: block;
    width: 16px;
    height: 16px;
  }
  
  .horizontal-line,
  .vertical-line {
    transform-origin: center;
    transition: transform 0.3s ease, opacity 0.3s ease;
  }
  
  .courses-grid {
    padding: 2rem;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
    transform-origin: top;
  }
  
  /* Transition styles for slide animation */
  .slide-enter-active,
  .slide-leave-active {
    transition: all 0.3s ease;
  }
  
  .slide-enter-from,
  .slide-leave-to {
    opacity: 0;
    transform: scaleY(0);
  }
  
  .slide-enter-to,
  .slide-leave-from {
    opacity: 1;
    transform: scaleY(1);
  }
  </style>