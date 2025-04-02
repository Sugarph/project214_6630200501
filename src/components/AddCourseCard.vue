<template>
  <div class="add-course-card" @click="handleClick">
    <div class="add-course-container">
      <div class="add-course-inner">
        <span>+</span>
        <p>Add Course</p>
      </div>
    </div>
  </div>
</template>

<script>
import { EventBus } from "@/event-bus.js";

export default {
  name: "AddCourseCard",
  props: {
    year: {
      type: Number,
      required: true
    }
  },
  methods: {
    handleClick() {
      console.log(`Adding course for year ${this.year}`);
      EventBus.emit("modal:open", { type: "addCourse", year: this.year });
    }
  }
};
</script>

<style scoped>
.add-course-card {
  position: relative;
  filter: drop-shadow(0 0 0 rgba(147, 51, 234, 0.5));
  transition: filter 0.3s ease;
  --card-color: #9333ea;
  cursor: pointer;
  /* Reduced height but kept width the same */
  width: 300px;
  height: 180px;  /* Reduced from 200px to 160px */
  min-width: 350px;
  min-height: 180px;  /* Reduced from 200px to 160px */
  max-width: 350px;
  max-height: 160px;  /* Reduced from 200px to 160px */
  flex: 0 0 auto; /* Don't grow or shrink */
}

.add-course-card:hover {
  filter: drop-shadow(0 0 15px rgba(147, 51, 234, 0.5));
}

.add-course-container {
  position: relative;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  padding: 4px;
  overflow: hidden;
  /* Fixed size to match parent */
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}

.add-course-container::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    45deg,
    transparent 30%,
    var(--card-color) 40%,
    var(--card-color) 60%,
    transparent 70%
  );
  opacity: 0.3;
  transform: rotate(0deg);
  transition: all 0.5s ease;
  z-index: 0;
}

.add-course-container:hover::before {
  transform: rotate(180deg);
  opacity: 0.4;
}

.add-course-container:hover {
  transform: translateY(-5px);
}

.add-course-inner {
  position: relative;
  background: rgb(25, 25, 25);
  border-radius: 8px;
  padding: 1.2rem;  /* Slightly reduced padding */
  z-index: 1;
  /* Fixed size to fill container */
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;  /* Slightly reduced gap */
}

.add-course-inner span {
  font-size: 2.8rem;  /* Slightly reduced font size */
  color: var(--card-color);
  transition: all 0.3s ease;
}

.add-course-inner p {
  color: #fff;
  font-size: 1.1rem;
  transition: all 0.3s ease;
  margin: 0;
  padding: 0;
}

.add-course-container:hover .add-course-inner span,
.add-course-container:hover .add-course-inner p {
  filter: brightness(1.2);
}
</style>