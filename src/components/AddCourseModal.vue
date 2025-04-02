<template>
  <div v-if="show" class="modal">
    <div class="modal-content">
      <form @submit.prevent="handleSubmit">
        <h3>Add New Course</h3>
        <input v-model="courseData.code" placeholder="Course Code" required />
        <input v-model="courseData.name" placeholder="Course Name" required />
        <input
          v-model.number="courseData.credits"
          type="number"
          placeholder="Credits"
          min="1"
          required
        />
        <select
          v-model="courseData.grade"
          required
          class="grade-select"
          :style="{ borderColor: gradeColor, color: gradeColor }"
        >
          <option value="" disabled selected>Select Grade</option>
          <option
            v-for="grade in grades"
            :key="grade"
            :value="grade"
            :style="{ color: getGradeColor(grade) }"
          >
            {{ grade }}
          </option>
        </select>
        <div class="grade-indicator" v-if="courseData.grade">
          <div class="grade-display" :style="{ backgroundColor: gradeColor }">
            {{ courseData.grade }}
          </div>
          <div class="grade-label">Selected Grade</div>
        </div>
        <div class="year-indicator">
          <span>Adding to Year {{ year }}</span>
        </div>
        <div class="form-actions">
          <button type="submit" :style="{ backgroundColor: gradeColor }">
            Add
          </button>
          <button type="button" @click="handleCancel">Cancel</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { EventBus } from "@/event-bus.js";

export default {
  name: "AddCourseModal",
  props: {
    show: {
      type: Boolean,
      default: false,
    },
    grades: {
      type: Array,
      default: () => [
        "A",
        "A-",
        "B+",
        "B",
        "B-",
        "C+",
        "C",
        "C-",
        "D+",
        "D",
        "F",
      ],
    },
    year: {
      type: Number,
      default: 2,
    },
  },
  data() {
    return {
      courseData: {
        code: "",
        name: "",
        credits: 3,
        grade: "",
      },
      gradeColors: {
        A: "#22c55e", // Bright green
        "A-": "#4ade80", // Green
        "B+": "#a3e635", // Light green
        B: "#bef264", // Yellow-green
        "B-": "#facc15", // Yellow
        "C+": "#fbbf24", // Light orange
        C: "#fb923c", // Orange
        "C-": "#f97316", // Dark orange
        "D+": "#ef4444", // Light red
        D: "#dc2626", // Red
        F: "#b91c1c", // Bright red
      },
    };
  },
  computed: {
    gradeColor() {
      return this.courseData.grade
        ? this.gradeColors[this.courseData.grade]
        : "#9333EA";
    },
  },
  methods: {
    handleSubmit() {
      if (this.isValidCourse()) {
        // Add the year from props when submitting
        EventBus.emit("course:add", {
          ...this.courseData,
          year: this.year, // Explicitly set from props
          gradeColor: this.getGradeColor(this.courseData.grade),
        });
        console.log(`Submitting course for year ${this.year}`);
        this.resetForm();
        EventBus.emit("modal:close", "addCourse");
      }
    },
    handleCancel() {
      EventBus.emit("modal:close", "addCourse");
      this.resetForm();
    },
    resetForm() {
      this.courseData = {
        code: "",
        name: "",
        credits: 3,
        grade: "",
      };
    },
    isValidCourse() {
      return (
        this.courseData.code &&
        this.courseData.name &&
        this.courseData.credits &&
        this.courseData.grade
      );
    },
    getGradeColor(grade) {
      return this.gradeColors[grade] || "#9333EA";
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  height: 100vh;
  width: 100vw;
}

.modal-content {
  background: rgb(25, 25, 25);
  padding: 2rem;
  border-radius: 12px;
  width: 100%;
  max-width: 500px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  position: relative;
  z-index: 10000;
  margin: 2rem;
}

.modal-content form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.modal-content h3 {
  color: #fff;
  font-size: 1.8rem;
  margin-bottom: 1rem;
  text-align: center;
}

input,
.grade-select {
  width: 100%;
  padding: 0.8rem 1rem;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 6px;
  color: #fff;
  font-size: 1rem;
  transition: all 0.3s ease;
}

input:focus,
.grade-select:focus {
  outline: none;
  border-color: #9333ea;
  background: rgba(255, 255, 255, 0.15);
}

.grade-select:focus {
  border-color: var(--grade-color, #9333ea);
}

.grade-select option {
  background: rgb(25, 25, 25);
  color: inherit;
}

.grade-indicator {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-top: -0.5rem;
}

.grade-display {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  color: white;
  font-size: 1.1rem;
  text-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.grade-label {
  color: #aaa;
  font-size: 0.9rem;
}

.form-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
  margin-top: 1rem;
}

.form-actions button {
  padding: 0.8rem 2rem;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  color: #fff;
}

.form-actions button[type="submit"] {
  background: #9333ea;
  border: none;
}

.form-actions button[type="submit"]:hover {
  filter: brightness(1.1);
  transform: translateY(-2px);
}

.form-actions button[type="button"] {
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.form-actions button[type="button"]:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-2px);
}

</style>
