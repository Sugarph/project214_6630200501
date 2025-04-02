<template>
    <span class="typewriter" ref="typewriter"></span>
  </template>
  
  <script>
  export default {
    name: 'TypewriterText',
    props: {
      words: {
        type: Array,
        required: true
      },
      useScramble: {
        type: Boolean,
        default: false
      },
      scrambleSpeed: {
        type: Number,
        default: 25
      },
      scrambleDuration: {
        type: Number,
        default: 80
      },
      lockSpeed: {
        type: Number,
        default: 25
      },
      deleteSpeed: {
        type: Number,
        default: 20
      },
      pauseFull: {
        type: Number,
        default: 2500
      },
      pauseEmpty: {
        type: Number,
        default: 150
      },
      startOnView: {
        type: Boolean,
        default: true
      }
    },
    mounted() {
      const typewriter = this.$refs.typewriter;
      let currentIndex = 0;
      let charIndex = 0;
      let isDeleting = false;
      const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  
      typewriter.textContent = '';
  
      const getRandomChar = () => alphabet[Math.floor(Math.random() * alphabet.length)];
  
      const scrambleChar = (targetChar, callback) => {
        let scrambleTime = 0;
        const scramble = () => {
          if (scrambleTime < this.scrambleDuration) {
            typewriter.textContent = this.words[currentIndex].substring(0, charIndex) + getRandomChar();
            scrambleTime += this.scrambleSpeed;
            setTimeout(scramble, this.scrambleSpeed);
          } else {
            typewriter.textContent = this.words[currentIndex].substring(0, charIndex + 1);
            callback();
          }
        };
        scramble();
      };
  
      const type = () => {
        const currentWord = this.words[currentIndex];
  
        if (isDeleting) {
          typewriter.textContent = currentWord.substring(0, charIndex);
          if (charIndex > 0) {
            charIndex--;
            setTimeout(type, this.deleteSpeed);
          } else {
            isDeleting = false;
            currentIndex = (currentIndex + 1) % this.words.length;
            setTimeout(type, this.pauseEmpty);
          }
        }  else {
        if (charIndex < currentWord.length) {
          if (this.useScramble) {
            // scramble effect
            scrambleChar(currentWord[charIndex], () => {
              charIndex++;
              if (charIndex <= currentWord.length) {
                setTimeout(type, this.lockSpeed);
              }
            });
          } else {
            // typewriter effect
            typewriter.textContent = currentWord.substring(0, charIndex + 1);
            charIndex++;
            if (charIndex <= currentWord.length) {
              setTimeout(type, this.lockSpeed);
            }
          }
        } else {
          typewriter.textContent = currentWord;
          isDeleting = true;
          setTimeout(type, this.pauseFull);
        }
        }
      };
  
      const startTyping = () => {
        currentIndex = 0;
        charIndex = 0;
        isDeleting = false;
        typewriter.textContent = ''; 
        setTimeout(type, 1000); 
      };
  
      if (this.startOnView) {
        const observer = new IntersectionObserver(
          (entries) => {
            entries.forEach(entry => {
              if (entry.isIntersecting) {
                startTyping();
                observer.unobserve(entry.target);
              }
            });
          },
          { root: null, rootMargin: '0px', threshold: 0.1 }
        );
        observer.observe(typewriter);
      } else {
        startTyping(); 
      }
    }
  };
  </script>
  
  <style scoped>
  .typewriter {
    font-size: 3rem;
    margin-left: 0.5rem;
    font-weight: 700;
    display: inline;
    white-space: nowrap;
    overflow: hidden;
    white-space: pre-line;
    line-height: 1.4;
  }
  </style>