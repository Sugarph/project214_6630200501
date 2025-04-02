<template>
  <div class="profile">
    <section class="section-profile">
      <div
        class="background-wrapper"
        :style="{ transform: `translateY(${-backgroundTranslate}px)` }"
      >
        <div
          class="section-inner"
          :style="{
            transform: `translate(-50%, -50%) translateY(${-backgroundTranslate}px)`,
            opacity: 1 - scrollProgress * 3.75,
          }"
        >
          <h4>About Me</h4>
          <h2>Phoorinut Hochuei</h2>
          <p>First glimpse into my world</p>
        </div>
        <scroll-arrow
          :translate-y="-backgroundTranslate"
          :opacity="1 - scrollProgress * 3.75"
        />
        <background-rotator :images="backgroundImages" />
      </div>
      <div
        class="overlay"
        :style="{
          transform: `translateY(${overlayTranslate}px)`,
        }"
        ref="overlay"
      >
        <div class="overlay-content">
          <div class="about-section">
            <div class="about-content">
              <h2>About & Talk with Me</h2>
              <p>
                Hello! My name is
                <span class="highlight">Phoorinut Hochuei</span>, but you can
                call me <span class="highlight">Sugar</span>. I'm a 19-year-old
                student at Kasetsart University Sriracha Campus. Currently I'm
                in my second year studying Computer Science. I graduated from
                Kasetsart University Laboratory School Center for Education
                Research and Development. Yeah, I know, long name. And yes, it's
                a Kasetsart-related school, well actually it's inside the
                university itself. So that's why I chose Sriracha Campus instead
                of the main one. Studying there for 16 years? That would be a
                heck of a long time (12 is already long enough). But I still go
                there almost every month tho since my friend studies there too.
                My dream job? Game Developer. But honestly, anything code
                related works for me.
              </p>

              <p>
                I <span class="highlight">LOVE</span> coding and anything
                related to space and technology. That's one of the reasons why
                I'm using a long-exposure Earth image as my background. Fun
                fact: The current background image is a Thai Aurora photo taken
                from the ISS by
                <a
                  href="https://x.com/astro_Pettit/status/1896900808073248852"
                  target="_blank"
                  class="link"
                  >Don Pettit</a
                >. And yes this website is heavily inspired by SpaceX website.
              </p>

              <p>
                I'm also an artist. I use Clip Studio Paint and I love watching
                my favorite streamer,
                <a
                  href="https://www.twitch.tv/vedal987"
                  target="_blank"
                  class="link"
                  >Neuro-sama</a
                >. But lately, I rarely draw. My favorite game?
                <a
                  href="https://www.paradoxinteractive.com/games/stellaris"
                  target="_blank"
                  class="link"
                  >Stellaris</a
                >. Space-related, who would've guessed? (ha) Oh, and as you can
                probably tell by now, I'm VERY good at English. (This is a
                flex.) In fact, I prefer typing in English over Thai and
                sometimes even talking too. Fun fact about me: I'm 162cm tall
                and a cosplayer, so almost every time I cosplay, people confuse
                me for a girl. (UwU, sorry)
              </p>

              <p>
                My hobby is watching streamers, usually just Neuro-sama and she
                is an AI streamer. Another fun fact: I've spent almost 100k baht
                for her. Oops, I guess (we're going AI overlord route with this)
              </p>

              <div class="media-box">
                <p>
                  I also have a daughter! Not a real one ofcourse, she's a
                  Vtuber! I drew the model for her and yes, she's an AI Vtuber.
                  Her story is quite long so I won't rant about it here.
                  Basically, it's just a running inside joke that somehow turned
                  real. This video pretty much sum up how she was born
                </p>
                <a
                  href="https://www.youtube.com/watch?v=nxNaGp1v3o8"
                  target="_blank"
                  class="video-link"
                >
                  <div class="video-thumbnail">
                    <i class="play-icon">▶</i>
                    <span>Here</span>
                  </div>
                </a>
              </div>
              <div class="social-links">
                <h3>Find me</h3>
                <div class="links-container">
                  <a
                    href="https://github.com/Sugarph"
                    target="_blank"
                    class="social-link"
                  >
                    <svg
                      class="social-icon github"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                      />
                    </svg>
                  </a>
                  <a
                    href="https://x.com/_SugarPh_"
                    target="_blank"
                    class="social-link"
                  >
                    <svg
                      class="social-icon twitter"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"
                      />
                    </svg>
                  </a>
                  <a
                    href="https://discordapp.com/users/Sugarph"
                    target="_blank"
                    class="social-link"
                  >
                    <svg
                      class="social-icon discord"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057 19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"
                      />
                    </svg>
                  </a>
                </div>
              </div>
            </div>

            <div class="about-image">
              <div class="profile-shape-container primary-hex">
                <img src="@/assets/myPicture.jpg" alt="Profile Picture" />
              </div>
              <div class="profile-shape-container secondary-hex">
                <img src="@/assets/myPicture2.jpg" alt="Secondary Picture" />
              </div>
              <div class="profile-shape-container tertiary-hex">
                <img src="@/assets/myPicture3.jpg" alt="Tertiary Picture" />
              </div>
            </div>
          </div>

          <div class="skills-section">
            <div class="section-title">
              <div class="line"></div>
              <h2>Skills</h2>
              <div class="line"></div>
            </div>
            <div class="skills-grid">
              <skill-hex
                v-for="skill in skills"
                :key="skill.name"
                :name="skill.name"
                :icon="skill.icon"
                :color="skill.color"
                :size="skill.size"
              />
            </div>
          </div>
          <div class="courses-section">
            <div class="section-title">
              <div class="line"></div>
              <h2>Grade & Courses</h2>
              <div class="line"></div>
            </div>

            <div class="content-row">
              <stat-number
                :value="currentCredits"
                label="Credit"
                position="left-content"
              />
              <gauge-chart :value="currentGPA" :maxValue="4" label="GPA" />
              <stat-number
                :value="currentYears"
                label="Years"
                position="right-content"
              />
            </div>
            <div class="line"></div>

            <div class="years-container">
              <year-section
                v-for="year in availableYears"
                :key="year"
                :year="year"
                :courses="courses"
                :initial-expanded="year === lastAddedYear"
              />
              <add-year-card v-if="availableYears.length < 6" />
            </div>
          </div>
        </div>
      </div>
      <add-course-modal
        :show="showAddCourseForm"
        :grades="grades"
        :year="currentYearForForm"
        @cancel="showAddCourseForm = false"
      />
    </section>
  </div>
</template>

<script>
import BackgroundRotator from "@/components/BackgroundRotator.vue";
import GaugeChart from "@/components/GaugeChart.vue";
import StatNumber from "@/components/StatNumber.vue";
import ScrollArrow from "@/components/ScrollArrow.vue";
import SkillHex from "@/components/SkillHex.vue";
import CourseCard from "@/components/CourseCard.vue";
import AddCourseModal from "@/components/AddCourseModal.vue";
import AddCourseCard from "@/components/AddCourseCard.vue";
import YearSection from "@/components/YearSection.vue";
import AddYearCard from "@/components/AddYearCard.vue";
import vueLogo from "@/assets/logo.svg";
import cssLogo from "@/assets/css.svg";
import jsLogo from "@/assets/js.svg";
import htmlLogo from "@/assets/html.svg";
import godotLogo from "@/assets/godot.svg";
import cppLogo from "@/assets/cpp.svg";
import pythonLogo from "@/assets/python.svg";
import csLogo from "@/assets/cs.svg";
import javaLogo from "@/assets/java.svg";
import cspLogo from "@/assets/csp.png";

import { EventBus } from "@/event-bus.js";

export default {
  components: {
    BackgroundRotator,
    GaugeChart,
    StatNumber,
    ScrollArrow,
    SkillHex,
    CourseCard,
    AddCourseModal,
    AddCourseCard,
    YearSection,
    AddYearCard,
  },
  data() {
    return {
      backgroundImages: [
        "https://pbs.twimg.com/media/GlMkt-CWwAAtLxW?format=jpg&name=large",
      ],
      skills: [
        { name: "Vue.js", icon: vueLogo, color: "#42b883" },
        { name: "CSS", icon: cssLogo, color: "#2965f1", size: 1.2 },
        { name: "Javascript", icon: jsLogo, color: "#f7df1e", size: 0.9 },
        { name: "HTML", icon: htmlLogo, color: "#e44d26", size: 1.2 },
        { name: "C++", icon: cppLogo, color: "#00599c", size: 1.25 },
        { name: "Python", icon: pythonLogo, color: "#3776ab" },
        { name: "Godot", icon: godotLogo, color: "#478cbf" },
        { name: "C#", icon: csLogo, color: "#239120", size: 0.9 },
        { name: "Java", icon: javaLogo, color: "#f89820" },
        { name: "Clip Studio Paint", icon: cspLogo, color: "#ff5c95" }, // cant find svg ;-;
      ],
      backgroundTranslate: 0,
      overlayTranslate: window.innerHeight,
      scrollProgress: 0,
      currentGPA: 0,
      currentCredits: 0,
      currentYears: 2,
      animationFrame: null,
      courses: [],
      showAddCourseForm: false,
      grades: ["A", "B+", "B", "C+", "C", "D+", "D", "F"],
      stats: { gpa: 0, credits: 0, years: 2 }, // Store calculated stats
      currentYearForForm: 2,
      availableYears: [1, 2],
      lastAddedYear: 2,
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
    this.fetchCourses();

    EventBus.on("course:add", this.addCourse);
    EventBus.on("course:update", this.updateCourse);
    EventBus.on("course:delete", this.deleteCourse);
    EventBus.on("modal:open", (data) => {
      if (typeof data === "object" && data.type === "addCourse") {
        this.showAddCourseForm = true;
        this.currentYearForForm = data.year;
      } else if (data === "addCourse") {
        this.showAddCourseForm = true;
        this.currentYearForForm = 2;
      }
    });
    EventBus.on("modal:close", () => {
      this.showAddCourseForm = false;
    });
    EventBus.on("year:add", this.addYear);
    EventBus.on("year:remove", this.removeYear);

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            this.animateStats(
              this.stats.gpa,
              this.stats.credits,
              this.stats.years
            );
          } else {
            this.currentGPA = 0;
            this.currentCredits = 0;
            this.currentYears = 0;
            if (this.animationFrame) {
              cancelAnimationFrame(this.animationFrame);
              this.animationFrame = null;
            }
          }
        });
      },
      { threshold: 0.025 }
    );

    observer.observe(this.$refs.overlay);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
    if (this.animationFrame) cancelAnimationFrame(this.animationFrame);
    EventBus.off("course:add", this.addCourse);
    EventBus.off("course:update", this.updateCourse);
    EventBus.off("course:delete", this.deleteCourse);
    EventBus.off("modal:open");
    EventBus.off("modal:close");
    EventBus.off("year:add");
    EventBus.off("year:remove");
  },
  methods: {
    async fetchSettings() {
      try {
        const response = await fetch("http://localhost:3000/settings");
        const settings = await response.json();

        if (settings && settings.availableYears) {
          this.availableYears = settings.availableYears;
          this.lastAddedYear =
            settings.lastAddedYear || Math.max(...settings.availableYears);
        }
      } catch (error) {
        console.error("Error fetching settings:", error);
        this.saveSettings();
      }
    },

    async saveSettings() {
      try {
        const settings = {
          availableYears: this.availableYears,
          lastAddedYear: this.lastAddedYear,
        };

        const response = await fetch("http://localhost:3000/settings", {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(settings),
        });

        if (!response.ok) {
          await fetch("http://localhost:3000/settings", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(settings),
          });
        }
      } catch (error) {
        console.error("Error saving settings:", error);
      }
    },

    async fetchCourses() {
      try {
        await this.fetchSettings();

        const response = await fetch("http://localhost:3000/courses");
        const data = await response.json();

        this.courses = data.map((course) => {
          if (!course.year) {
            const courseIndex = data.findIndex((c) => c.id === course.id);
            course.year = (courseIndex % 2) + 1;

            // Save the updated course with year back to the database
            this.updateCourseWithYear(course);
          }
          return course;
        });

        if (this.courses.length > 0) {
          // Find all years that have courses
          const yearsInUse = [
            ...new Set(this.courses.map((course) => course.year)),
          ];

          let yearsChanged = false;
          yearsInUse.forEach((year) => {
            if (!this.availableYears.includes(year)) {
              this.availableYears.push(year);
              yearsChanged = true;
            }
          });

          this.availableYears.sort((a, b) => a - b);

          if (this.availableYears.length > 0) {
            this.lastAddedYear = Math.max(...this.availableYears);
          }

          // Save changes to database if needed
          if (yearsChanged) {
            this.saveSettings();
          }
        }

        this.updateStats();
      } catch (error) {
        console.error("Error fetching courses:", error);
      }
    },

    async updateCourseWithYear(course) {
      try {
        await fetch(`http://localhost:3000/courses/${course.id}`, {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(course),
        });
      } catch (error) {
        console.error("Error updating course year:", error);
      }
    },

    async addCourse(courseData) {
      try {
        console.log("Adding course with data:", courseData);

        if (!courseData.year) {
          courseData.year = this.currentYearForForm;
          console.log("Added missing year:", courseData.year);
        }

        const response = await fetch("http://localhost:3000/courses", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(courseData),
        });

        const savedCourse = await response.json();
        console.log("Saved course:", savedCourse);

        if (!savedCourse.year && courseData.year) {
          savedCourse.year = courseData.year;
          console.log("Fixed missing year in saved course");
        }

        this.courses.push(savedCourse);
        this.updateStats();
        this.animateStats(this.stats.gpa, this.stats.credits, this.stats.years);
        this.showAddCourseForm = false;
      } catch (error) {
        console.error("Error adding course:", error);
      }
    },

    async updateCourse(updatedCourse) {
      try {
        const response = await fetch(
          `http://localhost:3000/courses/${updatedCourse.id}`,
          {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(updatedCourse),
          }
        );
        const savedCourse = await response.json();
        const index = this.courses.findIndex((c) => c.id === savedCourse.id);
        if (index !== -1) {
          this.courses[index] = savedCourse;
          this.updateStats();
          this.animateStats(
            this.stats.gpa,
            this.stats.credits,
            this.stats.years
          );
        }
      } catch (error) {
        console.error("Error updating course:", error);
      }
    },

    removeYear(year) {
      // Don't remove if:
      // year 1
      // there year higher
      if (
        this.availableYears.length <= 1 ||
        year === 1 ||
        this.availableYears.some((y) => y > year)
      ) {
        console.log("Cannot remove year:", year);
        if (year === 1) {
          console.log("  - Year 1 cannot be removed");
        } else if (this.availableYears.some((y) => y > year)) {
          console.log("  - Cannot remove year when higher years exist");
        } else {
          console.log("  - Cannot remove the only remaining year");
        }
        return;
      }

      console.log(`Removing empty year ${year}`);

      // Update available years
      this.availableYears = this.availableYears.filter((y) => y !== year);

      // Save to database
      this.saveSettings();

      // Update stats
      this.stats.years = this.availableYears.length;
      this.animateStats(this.stats.gpa, this.stats.credits, this.stats.years);
    },

    async deleteCourse(courseId) {
      try {
        await fetch(`http://localhost:3000/courses/${courseId}`, {
          method: "DELETE",
        });

        // Save the year before removing the course from the array
        const deletedCourse = this.courses.find(
          (course) => course.id === courseId
        );
        const yearOfDeletedCourse = deletedCourse?.year;

        this.courses = this.courses.filter((course) => course.id !== courseId);

        // Update stats
        this.updateStats();
        this.animateStats(this.stats.gpa, this.stats.credits, this.stats.years);

        // Check if this was the last course in a year (other than year 1)
        if (yearOfDeletedCourse && yearOfDeletedCourse > 1) {
          const coursesInYear = this.courses.filter(
            (course) => course.year === yearOfDeletedCourse
          );

          if (coursesInYear.length === 0) {
            this.removeYear(yearOfDeletedCourse);
          }
        }
      } catch (error) {
        console.error("Error deleting course:", error);
      }
    },
    addYear() {
      // Only add a new year if we don't already have it
      if (this.availableYears.length < 4) {
        const nextYear = Math.max(...this.availableYears) + 1;
        this.availableYears.push(nextYear);
        this.lastAddedYear = nextYear;

        // Save to database
        this.saveSettings();

        // Update years in stats
        this.stats.years = this.availableYears.length;
        this.animateStats(this.stats.gpa, this.stats.credits, this.stats.years);
      }
    },

    updateStats() {
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

      this.courses.forEach((course) => {
        totalCredits += Number(course.credits);
        totalGradePoints +=
          Number(course.credits) * (gradePoints[course.grade] || 0);
      });

      this.stats.gpa =
        totalCredits > 0
          ? Number((totalGradePoints / totalCredits).toFixed(2))
          : 0;
      this.stats.credits = totalCredits;

      this.stats.years = this.availableYears.length;

      // Animation will trigger via observer when overlay is visible
    },

    animateStats(newGPA, newCredits, newYears) {
      if (this.animationFrame) cancelAnimationFrame(this.animationFrame);

      const startGPA = this.currentGPA;
      const startCredits = this.currentCredits;
      const startYears = this.currentYears;
      let start = null;
      const duration = 1000; // 1 second animation

      const animate = (timestamp) => {
        if (!start) start = timestamp;
        const progress = Math.min((timestamp - start) / duration, 1);

        this.currentGPA = startGPA + (newGPA - startGPA) * progress;
        this.currentCredits = Math.round(
          startCredits + (newCredits - startCredits) * progress
        );
        this.currentYears = Math.round(
          startYears + (newYears - startYears) * progress
        );

        if (progress < 1) {
          this.animationFrame = requestAnimationFrame(animate);
        } else {
          this.currentGPA = newGPA;
          this.currentCredits = newCredits;
          this.currentYears = newYears;
        }
      };

      this.animationFrame = requestAnimationFrame(animate);
    },

    handleScroll() {
      const scrollY = window.scrollY;
      const windowHeight = window.innerHeight;
      const contentHeight =
        this.$refs.overlay.querySelector(".overlay-content").offsetHeight;

      const maxScroll = contentHeight + 150 - windowHeight;

      this.scrollProgress = Math.min(1, scrollY / (windowHeight * 0.3));
      this.backgroundTranslate = scrollY * 0.75;

      if (scrollY <= maxScroll) {
        this.overlayTranslate = windowHeight - 30 - scrollY * 1.5;
      } else {
        this.overlayTranslate = windowHeight - 30 - maxScroll * 1.5;
      }
    },
  },
};
</script>

<style scoped>
.profile {
  height: auto;
  min-height: 500vh;
  overflow: hidden;
  position: relative;
}

.background-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 1;
  transition: transform 0.1s linear;
  will-change: transform;
}

.overlay {
  position: fixed;
  top: 0px;
  left: 0;
  width: 100%;
  height: 1200vh;
  background: linear-gradient(
    to bottom,
    rgba(15, 15, 15, 0) 0%,
    rgb(12, 12, 12) 50px
  );
  z-index: 2;
  transition: transform 0.1s linear;
  will-change: transform;
}

.overlay-content {
  max-width: 1600px;
  margin: 50px auto 0;
  padding: 5rem 2rem;
  color: #fff;
  text-align: center;
}

.content-row {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.section-inner {
  color: #fff;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 3;
  width: 100%;
  text-align: center;
}

.section-inner h4 {
  font-size: 1.25rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 1rem;
}

.section-inner h2 {
  font-size: 3rem;
  margin: 0.5rem 0;
  font-weight: 700;
}

.section-inner p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

.about-section {
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 8rem;
  margin-top: 8rem;
  padding: 0 6rem;
  text-align: left;
  max-width: 100%;
}

.about-content {
  color: #ffffff;
  margin-left: -4rem;
  font-family: "Eurostile", sans-serif;
  line-height: 1.6;
}

.about-content h2 {
  font-size: 2.5rem;
  color: #ffffff;
  margin-bottom: 2rem;
  position: relative;
  display: inline-block;
}

.about-content h2::after {
  content: "";
  position: absolute;
  bottom: -10px;
  left: 0;
  width: 100%;
  height: 3px;
  background: linear-gradient(90deg, #ffffff, transparent);
}

.about-content p {
  margin-bottom: 1.5rem;
  font-size: 1.1rem;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.878);
  max-width: 95%;
}

.highlight {
  color: #ffffff;
  font-weight: 700;
}

.link {
  color: #ffffff;
  text-decoration: none;
  position: relative;
  padding-bottom: 2px;
  transition: all 0.3s ease;
  font-weight: 700;
  background-color: transparent;
}

.link::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 1px;
  background: #ffffff;
  transition: width 0.3s ease;
}

.link:hover {
  color: #ffffff;
}

.link:hover::after {
  width: 100%;
}

.media-box {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 1.5rem;
  margin: 2rem 0;
  border-left: 3px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  position: relative;
  max-width: 95%;
}

.media-box p {
  margin-bottom: 1rem;
}

.video-link {
  display: inline-block;
  text-decoration: none;
}

.video-thumbnail {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(255, 255, 255, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 8px;
  transition: all 0.3s ease;
  width: fit-content;
}

.video-thumbnail:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
}

.play-icon {
  color: #ffffff;
  font-size: 1.2rem;
}

.video-thumbnail span {
  color: #fff;
  font-weight: 500;
}

.social-links {
  margin-top: 3rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 1.5rem;
  max-width: 95%;
}

.social-links h3 {
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: #fff;
}

.links-container {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 50%;
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.social-link:hover {
  background: rgba(255, 255, 255, 0.14);
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.social-icon {
  width: 100%;
  height: 100%;
  fill: #fff;
  transition: fill 0.3s ease;
}

.social-icon.github:hover {
  fill: #fff;
}

.social-icon.twitter:hover {
  fill: #fff;
}

.social-icon.discord:hover {
  fill: #fff;
}

.about-image {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  margin-right: 0;
  margin-left: -2rem;
  position: relative;
  height: 600px;
  filter: drop-shadow(0 0 10px rgba(0, 0, 0, 0.5));
}

.profile-shape-container {
  position: absolute;
  width: 400px;
  height: 460px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  background: rgba(25, 25, 25, 0.95);
  animation: orbitPulse 16s infinite ease-in-out;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.primary-hex {
  top: 0;
  left: 0;
  z-index: 2;
}

.secondary-hex {
  top: 345px;
  left: 200px;
  z-index: 1;
}

/* Erhh why i name it this way?*/
.tertiary-hex {
  top: 0px;
  left: 400px;
  z-index: 1;
}

.profile-shape-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  clip-path: inherit;
  display: block;
  transition: all 0.4s ease;
  filter: brightness(0.9);
}

.profile-shape-container:hover img {
  transform: scale(1.025);
  filter: brightness(1.05);
}

.skills-section {
  margin-top: 10rem;
  padding: 0 6rem;
  width: 100%;
  max-width: 1400px;
  margin-left: auto;
  margin-right: auto;
  position: relative;
  z-index: 2;
}

.section-title {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 4rem;
}

.section-title h2 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #fff;
  white-space: nowrap;
}

.line {
  height: 2px;
  background: linear-gradient(
    to var(--direction, right),
    transparent,
    #fff 50%,
    transparent
  );
  flex: 1;
  margin: 1.5rem auto 2rem;
}

.line:first-child {
  --direction: right;
}

.line:last-child {
  --direction: left;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, 180px);
  gap: 4rem 3rem;
  max-width: 1200px;
  margin: 0 auto;
  justify-content: center;
  position: relative;
  z-index: 3;
}

.courses-section {
  margin-top: 15rem;
  padding: 0 6rem;
  width: 100%;
  max-width: 1400px;
  margin-left: auto;
  margin-right: auto;
  position: relative;
  z-index: 2;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.years-container {
  display: flex;
  flex-direction: column;
  max-width: 1200px;
  margin: 0 auto;
}

@keyframes orbitPulse {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-25px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
