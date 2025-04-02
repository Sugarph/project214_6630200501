<template>
  <div class="about">
    <section class="section-about">
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
          <h4>Projects & Art</h4>
          <h2>My Creative Works</h2>
          <p>A collection of my projects and artistic endeavors</p>
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
          <div class="projects-section">
            <div class="section-title">
              <div class="line"></div>
              <h2>Projects</h2>
              <div class="line"></div>
            </div>
            <p class="section-note">
              These are some of my favorite projects. I've worked on many more,
              but these are the ones I'm most proud of and some that I didn't upload to github.
            </p>
            <div class="projects-grid">
              <div
                class="project-card"
                v-for="project in projects"
                :key="project.id"
              >
                <div class="project-image-container">
                  <img
                    :src="project.image"
                    :alt="project.title"
                    class="project-image"
                  />
                </div>
                <div class="project-content">
                  <h3 class="project-title">{{ project.title }}</h3>
                  <div class="project-tech">
                    <span
                      class="tech-tag"
                      v-for="(tech, index) in project.technologies"
                      :key="index"
                    >
                      {{ tech }}
                    </span>
                  </div>
                  <p class="project-description">{{ project.description }}</p>
                  <div class="project-links">
                    <a
                      v-if="project.github"
                      :href="project.github"
                      target="_blank"
                      class="project-link github"
                    >
                      <svg
                        viewBox="0 0 24 24"
                        xmlns="http://www.w3.org/2000/svg"
                        class="link-icon"
                      >
                        <path
                          d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                        />
                      </svg>
                      Code
                    </a>
                    <a
                      v-if="project.demo"
                      :href="project.demo"
                      target="_blank"
                      class="project-link demo"
                    >
                      <svg
                        viewBox="0 0 24 24"
                        xmlns="http://www.w3.org/2000/svg"
                        class="link-icon"
                      >
                        <path
                          d="M14 3v2h3.59l-9.83 9.83 1.41 1.41L19 6.41V10h2V3m-2 16H5V5h7V3H5c-1.11 0-2 .89-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2v-7h-2v7z"
                        />
                      </svg>
                      Demo
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="art-section">
            <div class="section-title">
              <div class="line"></div>
              <h2>Art Archive</h2>
              <div class="line"></div>
            </div>
            <p class="section-note">
              This is just some of the art that I have created,I have a lot more, but upload them all here would be a pain.
            </p>
            <div class="art-grid">
              <a
                v-for="art in artworks"
                :key="art.id"
                :href="art.link"
                target="_blank"
                class="art-card-link"
              >
                <div class="art-card">
                  <div class="art-image-container">
                    <img :src="art.image" :alt="art.title" class="art-image" />
                  </div>
                  <div class="art-content">
                    <h3 class="art-title">{{ art.title }}</h3>
                    <p class="art-date">{{ art.date }}</p>
                    <p class="art-description">{{ art.description }}</p>
                    <div class="art-tags">
                      <span
                        class="art-tag"
                        v-for="(tag, index) in art.tags"
                        :key="index"
                      >
                        {{ tag }}
                      </span>
                    </div>
                  </div>
                </div>
              </a>
            </div>
          </div>
          <div class="bottom-spacer"></div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import BackgroundRotator from "@/components/BackgroundRotator.vue";
import ScrollArrow from "@/components/ScrollArrow.vue";

export default {
  components: {
    BackgroundRotator,
    ScrollArrow,
  },
  data() {
    return {
      backgroundImages: [
        "https://images.unsplash.com/photo-1501084817091-a4f3d1d19e07?auto=format&fit=crop&q=80",
      ],
      backgroundTranslate: 0,
      overlayTranslate: window.innerHeight,
      scrollProgress: 0,
      animationFrame: null,
      projects: [
        {
          id: 1,
          title: "Sugar Profile Website",
          image:
            "https://cdn.discordapp.com/attachments/1156504358826020884/1356994324923023501/image.png?ex=67ee96f2&is=67ed4572&hm=2b53395c86adbcda8ded17e73ae110086abc310558c7e42aeaae229124fee366&",
          technologies: ["Vue.js", "CSS", "JavaScript"],
          description:
            "Litterly this website, a personal portfolio showcasing my projects and art. An assignment for a Practicum in Software Development course.",
          github: "https://github.com/yourusername/sugar-profile",
        },
        {
          id: 2,
          title: "Escape The Maze Game",
          image:
            "https://cdn.discordapp.com/attachments/1156504358826020884/1356994083033186426/image.png?ex=67ee96b9&is=67ed4539&hm=8c8b8d356e21ed9d2c0eb9cc241ab13a6b7449cd796059068ba45e717bcb9da3&",
          technologies: ["Java", "Clip Studio Paint"],
          description:
            "An 3D 'Horror' game, It using pure Java and 'custom' game engine. Also It use Raycasting for 3D rendering.",
          github: "https://github.com/Sugarph/MazeGame",
        },
        {
          id: 3,
          title: "KUbot",
          image:
            "https://cdn.discordapp.com/attachments/1156504358826020884/1356993568618713339/image.png?ex=67ee963e&is=67ed44be&hm=5e24f687d4cbb7dbefdf440c72be89cccb234da4b2b82f064fb5d65bacd0ef50&",
          technologies: ["Python", "API"],
          description:
            "A discord bot for KU, That will spam you a reminder for your class schedule. It not finished and not planned to. Still a good project.",
          github:
            "https://github.com/Sugarph/Fundamental-Programming-Concepts-Project",
        },
        {
          id: 4,
          title: "Particle Life",
          image:
            "https://cdn.discordapp.com/attachments/1156504358826020884/1356994623838621757/image.png?ex=67ee973a&is=67ed45ba&hm=f5120bc3e44a6d363ea5d76aa12b1863eb946fd79aa2a27943162135d960573a&",
          technologies: ["C++"],
          description:
            "A simple particle system simulation. It was a project for my C++ course., sadly I don't have the source code anymore. and the picture is not mine, it for visualization what project is.",
          github: "",
        },
        {
          id: 5,
          title: "Fragment of an AI",
          image:
            "https://img.itch.zone/aW1nLzE0NTE0ODYwLnBuZw==/315x250%23c/MX1igz.png",
          technologies: ["Godot", "Clip Studio Paint"],
          description:
            "A boss rush game jam project, From Neuro-sama Game Jam 2023. With 3 days limit to develop it. it quite fun(sleep deprived) experience.",
          demo: "https://sugarph.itch.io/fragment-of-ai",
        },
      ],
      artworks: [
        {
          id: 1,
          title: "Neuro Cross Emote",
          image:
            "https://pbs.twimg.com/media/F5XnfrtbUAAOuF5?format=jpg&name=large",
          date: "September 2023",
          description:
            "An fan art emote of Neuro-sama, created for a discord. And it is actually become an official Twitch channel emote. Im very proud of this one.",
          tags: ["Fan Art", "Emote"],

          link: "https://x.com/_SugarPh_/status/1699518975988961734",
        },
        {
          id: 2,
          title: "Evil Reflection",
          image:
            "https://pbs.twimg.com/media/GJkDGeWa0AA0Lhk?format=jpg&name=4096x4096",
          date: "March 2024",
          description:
            "Fan art portrait of Evil Neuro-sama sister of Neuro,In a mirror. It for her birthday.",
          tags: ["Portrait", "Fan Art"],

          link: "https://x.com/_SugarPh_/status/1772451406483435992",
        },
        {
          id: 3,
          title: "HBD Neuro",
          image:
            "https://pbs.twimg.com/media/GBvN5QUbYAAwFyP?format=jpg&name=large",
          date: "December 2023",
          description:
            "Fan art of Neuro-sama, celebrating her birthday.I quite a rush one since I have to finish it before the game jam start.",
          tags: ["Speed Art", "Fan Art"],

          link: "https://x.com/_SugarPh_/status/1737208472234791226",
        },
        {
          id: 4,
          title: "Neuro Lantern Festival",
          image:
            "https://pbs.twimg.com/media/F_7cD4oakAANMG2?format=jpg&name=large",
          date: "November 2023",
          description:
            "Neuro-sama in a lantern festival.With Thai traditional dress.",
          tags: ["Fan Art"],

          link: "https://x.com/_SugarPh_/status/1729061299118829634",
        },
        {
          id: 5,
          title: "Melba Toast",
          image:
            "https://cdn.discordapp.com/attachments/1156504358826020884/1357002549483274300/image.png?ex=67ee9e9b&is=67ed4d1b&hm=88770b101a45d3896cc81c8992b0e8ab7648912f459a2e53cb9b7e9190d3a9a1&",
          date: "October 2023",
          description:
            "My precious daughter, Melba Toast. She is a Vtuber from community project. I love her so much. and possibly one of my most time consuming project. ~80 hours.",
          tags: ["Live2D", "Vtuber", "Vtuber Model"],

          link: "https://www.twitch.tv/melbathetoast",
        },
        {
          id: 6,
          title: "Neuro-sama Lag Train MV",
          image:
            "https://media1.tenor.com/m/sF_gQKhjWqYAAAAd/neurosama-lagtrain.gif",
          date: "May 2023",
          description:
            "A fan art MV of Lag Train, a song by Neuro-sama. This is one of the first time I ever do an animation.",
          tags: ["Fan Art", "Animation"],
          link: "https://www.youtube.com/watch?v=uufsSYDtuCA&ab",
        },
      ],
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
    if (this.animationFrame) cancelAnimationFrame(this.animationFrame);
  },
  methods: {
    handleScroll() {
      const scrollY = window.scrollY;
      const windowHeight = window.innerHeight;
      const contentHeight =
        this.$refs.overlay.querySelector(".overlay-content").offsetHeight;

      const maxScroll = contentHeight + 150 - windowHeight + 100;

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
.about {
  height: auto;
  min-height: 310vh;
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
  height: 600vh;
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

.projects-section {
  margin-top: 8rem;
  padding: 0 6rem;
  width: 100%;
  max-width: 1400px;
  margin-left: auto;
  margin-right: auto;
  position: relative;
  z-index: 2;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2.5rem;
  max-width: 1200px;
  margin: 0 auto;
}

.project-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.3s ease;
  height: 100%;
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
  background: rgba(255, 255, 255, 0.08);
}

.project-image-container {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.project-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.project-card:hover .project-image {
  transform: scale(1.05);
}

.project-content {
  padding: 1.5rem;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.project-title {
  font-size: 1.4rem;
  margin-bottom: 0.8rem;
  font-weight: 600;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tech-tag {
  font-size: 0.85rem;
  padding: 0.25rem 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  display: inline-block;
}

.project-description {
  font-size: 0.95rem;
  line-height: 1.5;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 1.5rem;
  flex: 1;
}

.project-links {
  display: flex;
  gap: 1rem;
  margin-top: auto;
}

.project-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 6px;
  text-decoration: none;
  color: #fff;
  font-size: 0.9rem;
  transition: all 0.2s ease;
}

.project-link:hover {
  background: rgba(255, 255, 255, 0.15);
}

.link-icon {
  width: 18px;
  height: 18px;
  fill: #fff;
}

.art-section {
  margin-top: 15rem;
  padding: 0 6rem;
  width: 100%;
  max-width: 1400px;
  margin-left: auto;
  margin-right: auto;
  position: relative;
  z-index: 2;
}

.art-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
  max-width: 1200px;
  margin: 0 auto;
}

.art-card-link {
  text-decoration: none;
  color: inherit;
  display: block;
  cursor: pointer;
  background-color: #ffffff00;
}

.art-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  text-align: left;
  height: 100%;
}

.art-card-link:hover .art-card {
  transform: translateY(-8px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
  background: rgba(255, 255, 255, 0.08);
}

.art-image-container {
  width: 100%;
  height: 250px;
  overflow: hidden;
  position: relative;
}

.art-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.art-card-link:hover .art-image {
  transform: scale(1.05);
}

.art-content {
  padding: 1.5rem;
}

.art-title {
  font-size: 1.3rem;
  margin-bottom: 0.4rem;
  font-weight: 600;
}

.art-date {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.6);
  margin-bottom: 0.8rem;
}

.art-description {
  font-size: 0.95rem;
  line-height: 1.5;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 1rem;
}

.art-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.art-tag {
  font-size: 0.85rem;
  padding: 0.2rem 0.6rem;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  display: inline-block;
}

.section-note {
  max-width: 800px;
  margin: 0 auto 3rem;
  font-size: 1rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.7);
  font-style: italic;
}

.bottom-spacer {
  height: 120px;
}
</style>
