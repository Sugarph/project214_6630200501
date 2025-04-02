<template>
  <div class="course-card" :style="{ '--shadow-color': shadowColor }">
    <div
      class="card-container"
      :style="{
        '--card-color': course.gradeColor || getGradeColor(course.grade),
      }"
    >
      <div v-if="showDeleteConfirm" class="delete-confirm">
        <div class="confirm-message">Delete this course?</div>
        <div class="confirm-actions">
          <button class="confirm-btn" @click="confirmDelete">Delete</button>
          <button class="cancel-btn" @click="cancelDelete">Cancel</button>
        </div>
      </div>
      <div class="card-inner">
        <div v-if="!editing" class="card-content">
          <div class="course-header">
            <h3>{{ course.code }}</h3>
            <div class="actions">
              <button @click="startEdit" class="action-btn">Edit</button>
              <button @click="handleDelete" class="action-btn delete">×</button>
            </div>
          </div>
          <p class="course-name">{{ course.name }}</p>
          <div class="course-details">
            <span>Credits: {{ course.credits }}</span>
            <span class="grade">Grade: {{ course.grade }}</span>
          </div>
        </div>
        <form v-else @submit.prevent="handleSave" class="edit-form">
          <input
            v-model="editedCourse.code"
            placeholder="Course Code"
            required
          />
          <input
            v-model="editedCourse.name"
            placeholder="Course Name"
            required
          />
          <input
            v-model.number="editedCourse.credits"
            type="number"
            placeholder="Credits"
            min="1"
            required
          />
          <select v-model="editedCourse.grade" required class="grade-select">
            <option value="" disabled>Select Grade</option>
            <option v-for="grade in grades" :key="grade" :value="grade">
              {{ grade }}
            </option>
          </select>
          <div class="form-actions">
            <button type="submit">Save</button>
            <button type="button" @click="cancelEdit">Cancel</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { EventBus } from "@/event-bus.js";

export default {
  name: "CourseCard",
  props: {
    course: {
      type: Object,
      required: true,
    },
  },
  computed: {
    shadowColor() {
      const color =
        this.course.gradeColor || this.getGradeColor(this.course.grade);
      return color || "#9333EA";
    },
  },
  data() {
    return {
      editing: false,
      editedCourse: null,
      grades: ["A", "B+", "B", "C+", "C", "D+", "D", "F"],
      showDeleteConfirm: false,
    };
  },
  methods: {
    getGradeColor(grade) {
      const gradeColors = {
        A: "#22c55e", // Bright green
        "B+": "#a3e635", // Light green
        B: "#bef264", // Yellow-green
        "C+": "#fbbf24", // Light orange
        C: "#fb923c", // Orange
        "D+": "#ef4444", // Light red
        D: "#dc2626", // Red
        F: "#b91c1c", // Bright red
      };
      return gradeColors[grade] || "#9333EA";
    },
    startEdit() {
      this.editedCourse = { ...this.course };
      this.editing = true;
    },
    handleSave() {
      if (this.isValidCourse()) {
        EventBus.emit("course:update", this.editedCourse);
        this.editing = false;
      }
    },
    handleDelete() {
      this.showDeleteConfirm = true;
    },
    confirmDelete() {
      EventBus.emit("course:delete", this.course.id);
      this.showDeleteConfirm = false;
    },
    cancelDelete() {
      this.showDeleteConfirm = false;
    },
    cancelEdit() {
      this.editing = false;
      this.editedCourse = null;
    },
    isValidCourse() {
      return (
        this.editedCourse.code &&
        this.editedCourse.name &&
        this.editedCourse.credits &&
        this.editedCourse.grade
      );
    },
  },
};
</script>

<style scoped>
.course-card {
  position: relative;
  filter: drop-shadow(0 0 0 var(--shadow-color, rgba(147, 51, 234, 0.15)));
  transition: filter 0.3s ease;
  --card-color: #9333ea;
}

.course-card:hover {
  filter: drop-shadow(0 0 15px var(--shadow-color, rgba(147, 51, 234, 0.15)));
}

.card-container {
  position: relative;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  padding: 4px;
  overflow: hidden;
}

.card-container::before {
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

.card-container:hover::before {
  transform: rotate(180deg);
  opacity: 0.4;
}

.card-container:hover {
  transform: translateY(-5px);
}

.card-inner {
  position: relative;
  background: rgb(25, 25, 25);
  border-radius: 8px;
  padding: 1.5rem;
  z-index: 1;
}

.card-content,
.edit-form {
  position: relative;
  z-index: 2;
}

.course-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.course-header h3 {
  color: var(--card-color);
  font-size: 1.5rem;
  font-weight: 700;
  transition: all 0.3s ease;
}

.course-card:hover .course-header h3 {
  filter: brightness(1.2);
}

.actions {
  display: flex;
  gap: 0.5rem;
}

.action-btn {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #fff;
  cursor: pointer;
  padding: 0.25rem 0.75rem;
  border-radius: 4px;
  transition: all 0.3s ease;
}

.action-btn:hover {
  background: var(--card-color);
  border-color: var(--card-color);
}

.action-btn.delete:hover {
  background: #ff4444;
  border-color: #ff4444;
}

.course-name {
  color: #fff;
  font-size: 1.1rem;
  margin-bottom: 1rem;
  transition: all 0.3s ease;
}

.course-card:hover .course-name {
  filter: brightness(1.2);
}

.course-details {
  display: flex;
  justify-content: space-between;
  color: #888;
  font-size: 0.9rem;
  transition: all 0.3s ease;
}

.grade {
  color: var(--card-color);
  font-weight: 600;
}

.edit-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.edit-form input,
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

.edit-form input:focus,
.grade-select:focus {
  outline: none;
  border-color: var(--card-color);
  background: rgba(255, 255, 255, 0.15);
}

.grade-select option {
  background: rgb(25, 25, 25);
  color: #fff;
  padding: 0.5rem;
}

.form-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
  margin-top: 0.5rem;
}

.form-actions button {
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.form-actions button[type="submit"] {
  background: var(--card-color);
  color: #fff;
  border: none;
}

.form-actions button[type="submit"]:hover {
  filter: brightness(1.2);
}

.form-actions button[type="button"] {
  background: transparent;
  color: #fff;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.form-actions button[type="button"]:hover {
  border-color: var(--card-color);
  background: rgba(147, 51, 234, 0.1);
}

.delete-confirm {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 5;
  padding: 1.5rem;
  backdrop-filter: blur(4px);
  animation: fadeIn 0.2s ease-out;
}

.confirm-message {
  color: white;
  font-size: 1.2rem;
  margin-bottom: 1.5rem;
  text-align: center;
}

.confirm-actions {
  display: flex;
  gap: 1rem;
}

.confirm-btn, .cancel-btn {
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
  border: none;
}

.confirm-btn {
  background-color: #ef4444; 
  color: white;
}

.confirm-btn:hover {
  background-color: #dc2626;
  transform: translateY(-2px);
}

.cancel-btn {
  background-color: rgba(255, 255, 255, 0.2);
  color: white;
}

.cancel-btn:hover {
  background-color: rgba(255, 255, 255, 0.3);
  transform: translateY(-2px);
}
</style>
