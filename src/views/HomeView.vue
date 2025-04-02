<template>
  <div class="home">
    <!-- Section 1 -->
    <section class="section-a">
      <background-rotator
        :images="[
          'https://pbs.twimg.com/media/GlMkt-CWwAAtLxW?format=jpg&name=large',
        ]"
      />
      <div class="section-inner">
        <h4>Welcome</h4>
        <h2>
          Hi, I'm
          <typewriter-text
            :words="['Phoorinut Hochuei', 'Sugar', 'ภูริณัฐ โห้เฉื่อย']"
            :start-on-view="true"
            :use-scramble="true"
          />
        </h2>

        <!-- Replace the static text with these animated elements -->
        <div class="student-info">
          <div class="student-badge fade-in">
            <span class="badge-label">Section</span>
            <span class="badge-value">S05</span>
          </div>
          <div class="student-badge fade-in">
            <span class="badge-label">ID</span>
            <span class="badge-value">6630200501</span>
          </div>
        </div>

        <animated-button tag="router-link" to="/profile" class="fade-in">
          Learn More
        </animated-button>
      </div>

      <scroll-arrow @click="scrollToNextSection" />
    </section>

    <!-- Section 2 -->
    <section class="section-b">
      <background-rotator :images="backgroundImages" />
      <div class="section-inner">
        <h4>My School</h4>
        <h2>
          <typewriter-text
            :words="[
              'Kasetsart University Laboratory School \n Center for Education Research and Development',
              'โรงเรียนสาธิตแห่งมหาวิทยาลัยเกษตรศาสตร์ \nศูนย์วิจัยและพัฒนาการศึกษา',
            ]"
            :pause-full="4500"
            :delete-speed="25"
          />
        </h2>
        <animated-button
          tag="a"
          href="https://www.kus.ku.ac.th/"
          target="_blank"
          class="fade-in"
        >
          Explore
        </animated-button>
      </div>
      <scroll-arrow @click="scrollToNextSection" />
    </section>

    <!-- Section 3 -->
    <section class="section-c">
      <div class="section-inner">
        <h4>My Archive</h4>
        <h2>Projects & Art</h2>
        <p>Some of my art and project that Im pround of.</p>
        <animated-button tag="router-link" to="/about" class="fade-in">
          View Details
        </animated-button>
      </div>
    </section>
  </div>
</template>

<script>
import TypewriterText from "@/components/TypewriterText.vue";
import BackgroundRotator from "@/components/BackgroundRotator.vue";
import ScrollArrow from "@/components/ScrollArrow.vue";
import AnimatedButton from "@/components/AnimatedButton.vue";
import kus1 from "@/assets/kus.jpg";
import kus2 from "@/assets/kus2.jpg";
import kus3 from "@/assets/kus3.jpg";

export default {
  components: {
    TypewriterText,
    BackgroundRotator,
    ScrollArrow,
    AnimatedButton,
  },
  data() {
    return {
      backgroundImages: [kus1, kus2, kus3],
    };
  },
  mounted() {
    const observerOptions = {
      root: null,
      rootMargin: "0px",
      threshold: 0.1,
    };

    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("fade-in");
        } else {
          entry.target.classList.remove("fade-in");
        }
      });
    }, observerOptions);

    // Update selector to be more specific
    document
      .querySelectorAll(
        ".section-inner h4, .section-inner h2, .section-inner p, .animated-btn.fade-in, .student-badge.fade-in",
        
      )
      .forEach((element) => {
        observer.observe(element);
      });
  },
  methods: {
    scrollToNextSection() {
      const currentSection = this.$el
        .querySelector(":hover")
        .closest("section");
      if (!currentSection) return;

      const nextSection = currentSection.nextElementSibling;
      if (!nextSection) return;

      const container = this.$el;
      const targetOffset = nextSection.offsetTop;

      container.scrollTo({
        top: targetOffset,
        behavior: "smooth",
      });
    },
  },
};
</script>

<style scoped>
.home {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  overflow-x: hidden;
  scroll-snap-type: y mandatory;
  scroll-behavior: smooth;
  margin: 0;
  padding: 0;
}

.home::-webkit-scrollbar {
  display: none;
}

section {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #fff;
  text-align: center;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  scroll-snap-align: start;
  position: relative;
}

::selection {
  background: rgba(255, 255, 255);
  color: #000000;
}

.section-a {
  position: relative;
}

.section-a::before {
  display: none;
}

.section-b {
  position: relative;
}

.section-c {
  background-image: url("https://images.unsplash.com/photo-1462331940025-496dfbfc7564?q=80&w=2711&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D");
}

.section-inner {
  padding: 2rem;
}

.section-inner span {
  font-weight: 700;
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
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  color: #fff;
}

.section-inner p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}
.animated-btn {
  opacity: 0;
}

.fade-in {
  opacity: 0;
  animation: fadeIn 0.75s ease-out forwards;
  animation-delay: 0.3s;
}

.animated-btn.fade-in {
  animation-delay: 0.5s;
}

.student-info {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  margin-bottom: 2rem;
  opacity: 1;
}

.student-badge {
  background: rgba(255, 255, 255, 0);
  backdrop-filter: blur(8px);
  border: 1px solid rgb(255, 255, 255);
  border-radius: 5px;
  padding: 0.7rem 1.2rem;
  display: flex;
  flex-direction: column;
  min-width: 120px;
  transform: translateY(10px);
  transition: all 0.3s ease;
  opacity: 0;
}

.badge-label {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  opacity: 1;
  margin-bottom: 0.3rem;
}

.badge-value {
  font-size: 1.1rem;
  font-weight: 600;
  letter-spacing: 1px;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(70px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
