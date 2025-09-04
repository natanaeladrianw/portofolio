<template>
  <main
    class="mt-10 md:mt-1 flex flex-col-reverse gap-8 items-center md:flex-row md:gap-16 md:justify-center min-h-[65vh] md:min-h-[80vh]">
    <div class="space-y-2 text-center md:text-left px-10">
      <p class="text-blue-400">{{ i18n.t ? i18n.t('hello_world_im') : 'Hello World, I\'m' }}</p>
      <h1 class="text-4xl font-bold md:text-5xl text-black dark:text-white fadein-up">Nathanael Adrian Wirawan</h1>
      <div class="py-2">
        <h1
          class="typewrite text-xl font-semibold text-transparent bg-clip-text bg-gradient-to-r from-blue-300 via-blue-500 to-blue-800 md:text-2xl fadein-up"
          ref="typewriter">
          <span class="wrap">{{ txt }}</span>
        </h1>
      </div>
      <p class="text-black dark:text-gray-200 pr-4 fade-in-from-left">{{ i18n.t ? i18n.t('welcome') : 'Welcome to My personal website.' }} <span class="wave">👋🏼</span></p>
      <br>
    </div>
    <div class="flex justify-center md:justify-start fadein-right">
      <img :src="avatarSrc" alt="avatar" width="300" height="300" decoding="async"
           class="w-10/12 md:h-auto rounded-full border-4 border-blue-400 pict" />
    </div>
  </main>
</template>

<script>
export default {
  inject: ['i18n'],
  name: 'HomeView',
  data() {
    return {
      toRotate: [],
      period: 2000,
      txt: '',
      loopNum: 0,
      isDeleting: false,
      avatarSrc: '/img/myfoto.jpg'
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.resetRotate();
      this.tick();
      this.tryOtherAvatarExtensions();
    });
  },
  methods: {
    resetRotate() {
      const t = this.i18n && this.i18n.t ? this.i18n.t.bind(this.i18n) : (k)=>k
      this.toRotate = [
        t('web_developer'),
        t('full_stack_engineer'),
        t('business_informatics_student'),
        t('tech_enthusiast')
      ];
      this.loopNum = 0;
      this.txt = '';
      this.isDeleting = false;
    },
    tryOtherAvatarExtensions() {
      const candidates = [
        '/img/myfoto.jpg',
        '/img/myfoto.jpeg',
        '/img/myfoto.png',
        '/img/myfoto.webp'
      ];
      const test = (idx) => {
        if (idx >= candidates.length) return;
        const img = new Image();
        img.onload = () => { this.avatarSrc = candidates[idx]; };
        img.onerror = () => test(idx + 1);
        img.src = candidates[idx] + '?v=' + Date.now();
      };
      test(0);
    },
    tick() {
      let typewriter = this.$refs.typewriter;

      if (!typewriter) {
        return;
      }

      let i = this.loopNum % this.toRotate.length;
      let fullTxt = this.toRotate[i];

      this.txt = this.isDeleting ? fullTxt.substring(0, this.txt.length - 1) : fullTxt.substring(0, this.txt.length + 1);
      typewriter.innerHTML = `<span class="wrap">${this.txt}</span>`;

      let that = this;
      let delta = 200 - Math.random() * 100;

      if (this.isDeleting) {
        delta /= 2;
      }

      if (!this.isDeleting && this.txt === fullTxt) {
        delta = this.period;
        this.isDeleting = true;
      } else if (this.isDeleting && this.txt === '') {
        this.isDeleting = false;
        this.loopNum++;
        delta = 500;
      }

      setTimeout(() => {
        that.tick();
      }, delta);
    },
  }
}
</script>

<style>
body {
  overflow-y: scroll;
  overflow-x: hidden;
}

.typewrite>.wrap {
  border-right: 0.08em solid #fff;
}

.wave {
  animation-name: wave-animation;
  animation-duration: 2.5s;
  animation-iteration-count: infinite;
  transform-origin: 70% 70%;
  display: inline-block
}

@keyframes wave-animation {
  0% {
    transform: rotate(0deg)
  }

  10% {
    transform: rotate(14deg)
  }

  20% {
    transform: rotate(-8deg)
  }

  30% {
    transform: rotate(14deg)
  }

  40% {
    transform: rotate(-4deg)
  }

  50% {
    transform: rotate(10deg)
  }

  60% {
    transform: rotate(0deg)
  }

  to {
    transform: rotate(0deg)
  }
}

.pict {
  box-shadow: 0 0 25px 5px rgba(59,130,246,0.8), /* biru terang */
              0 0 50px 10px rgba(37,99,235,0.6); /* biru lebih gelap */
  -webkit-box-shadow: 0 0 25px 5px rgba(59,130,246,0.8),
                      0 0 50px 10px rgba(37,99,235,0.6);
  -moz-box-shadow: 0 0 25px 5px rgba(59,130,246,0.8),
                   0 0 50px 10px rgba(37,99,235,0.6);
}

.fadein-up {
  opacity: 0;
  animation-name: fadeInUp;
  animation-duration: 0.5s;
  animation-fill-mode: forwards;
  animation-delay: 500ms;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

.fade-in-from-left {
  opacity: 0;
  animation: fadeInLeft 0.5s ease-out forwards;
  animation-delay: 500ms;
}

@keyframes fadeInLeft {
  0% {
    opacity: 0;
    transform: translateX(-100%);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

.fadein-right {
  opacity: 0;
  animation: fadeInRight 0.5s ease-out forwards;
  animation-delay: 500ms;
}

@keyframes fadeInRight {
  0% {
    opacity: 0;
    transform: translateX(100%);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

.fadein-bot {
  opacity: 0;
  animation: fadeInBot 0.5s forwards;
}

@keyframes fadeInBot {
  from {
    opacity: 0;
    transform: translate3d(0, -100%, 0);
  }

  to {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

.fadein-1 {
  animation-delay: 200ms;
}
.fadein-2 {
  animation-delay: 400ms;
}
.fadein-3 {
  animation-delay: 600ms;
}
.fade-500 {
  animation-delay: 500ms;
}
</style>
