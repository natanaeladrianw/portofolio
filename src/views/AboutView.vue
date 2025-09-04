<script>
export default {
  inject: ['i18n'],
  data() {
    return {
      activeTab: 1,
      tech: [
        {
          id: 1,
          name: 'HTML',
          imageUrl: 'https://cdn-icons-png.flaticon.com/512/1051/1051277.png',
          statusKey: 'advanced'
        },
        {
          id: 2,
          name: 'CSS',
          imageUrl: 'https://cdn-icons-png.flaticon.com/512/732/732190.png',
          statusKey: 'advanced'
        },
        {
          id: 3,
          name: 'PHP',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-php-2038871-1720084.png',
          statusKey: 'advanced'
        },
        {
          id: 4,
          name: 'Javascript',
          imageUrl: 'https://cdn.icon-icons.com/icons2/2415/PNG/512/javascript_original_logo_icon_146455.png',
          statusKey: 'intermediate'
        },
        {
          id: 5,
          name: 'Laravel',
          imageUrl: 'https://cdn.worldvectorlogo.com/logos/laravel-2.svg',
          statusKey: 'advanced'
        },
        {
          id: 6,
          name: 'VueJS',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-vue-282497.png?f=webp',
          statusKey: 'beginner'
        },
        {
          id: 7,
          name: 'Python',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-python-2-226051.png',
          statusKey: 'intermediate'
        },
        {
          id: 8,
          name: 'Tailwind',
          imageUrl: 'https://upload.wikimedia.org/wikipedia/commons/d/d5/Tailwind_CSS_Logo.svg',
          statusKey: 'beginner'
        },
        {
          id: 9,
          name: 'Bootstrap',
          imageUrl: 'https://getbootstrap.com/docs/5.2/assets/brand/bootstrap-logo-shadow.png',
          statusKey: 'advanced'
        },
        {
          id: 10,
          name: 'Kotlin',
          imageUrl: 'https://upload.wikimedia.org/wikipedia/commons/7/74/Kotlin_Icon.png',
          statusKey: 'intermediate'
        },
        {
          id: 11,
          name: 'Java',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-java-60-1174953.png',
          statusKey: 'intermediate'
        },
        {
          id: 12,
          name: 'SQL',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-mysql-3628940-3030165.png',
          statusKey: 'advanced'
        }
      ],
      tools: [
        {
          id: 1,
          name: 'Git',
          imageUrl: 'https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png',
          statusKey: 'version_control'
        },
        {
          id: 2,
          name: 'GitHub',
          imageUrl: 'https://cdn-icons-png.flaticon.com/512/25/25231.png',
          statusKey: 'git_hosting'
        },
        {
          id: 3,
          name: 'NPM',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-npm-3-1175132.png',
          statusKey: 'package_manager'
        },
        {
          id: 4,
          name: 'MySQL',
          imageUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-mysql-3628940-3030165.png',
          statusKey: 'database'
        },
      ]
    };
  },
  methods: {
    downloadCV() {
      const link = document.createElement('a');
      link.href = '/Nathanael Adrian Wirawan - CV.pdf';
      link.download = 'Nathanael Adrian Wirawan - CV.pdf';
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
}
</script>
<template>
  <div
    class="bg-gray-800 px-5 py-5 md:px-12 md:py-10 text-left border border-blue-400 rounded-3xl text-amber-50 mx-3 mb-5">
    <article data-page="about">

      <header>
        <div class="text-2xl font-bold text-white mb-5 fadein-bot title-section flex items-center">
          {{ i18n.t ? i18n.t('about_me') : 'About Me' }} &nbsp;
          <div class="h-[1px] w-32 bg-blue-400 md:w-96 aos-init aos-animate" data-aos="zoom-in-left"
            data-aos-duration="600"></div>
        </div>
      </header>

      <section
        class="text-sm md:text-lg text-justify flex flex-col gap-4 md:flex-row md:gap-8 md:justify-left md:items-center">
        <div class="flex justify-center">
          <img class="w-9/12 rounded-full mb-3 fadein-up"
            src="/img/myfoto.jpg" alt="Foto">
        </div>
        <div class="md:w-7/12">
          <p class="mb-3 md:mb-7 fadein-left fadeins-1">
            &nbsp; &nbsp; &nbsp; {{ i18n.t ? i18n.t('about_me_paragraph1') : 'Hi everyone! My name is Nathanael Adrian Wirawan. I am a web and mobile developer with experience in building applications using technologies such as HTML, CSS, JavaScript, PHP, Laravel, Vue.js, Python, Kotlin, and Java. I am passionate about creating digital solutions that are not only functional but also efficient and visually appealing. For me, programming is not just a skill, but also a form of creativity that brings ideas to life.' }}
          </p>
          <p class="mb-3 fadein-left fadeins-2">
            &nbsp; &nbsp; &nbsp; {{ i18n.t ? i18n.t('about_me_paragraph2') : 'My focus is to develop applications and websites that are user-friendly, responsive, and tailored to the client\'s needs. I also pay attention to design and usability, ensuring that every project delivers both value and satisfaction. My goal is to help businesses and individuals convey their message effectively through technology. If you are interested in collaborating with me, please feel free to reach out through the contact listed.' }}
          </p>
          <div class="mt-4 fadein-left fadeins-3">
            <button @click="downloadCV" class="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors duration-200 text-sm font-medium flex items-center gap-2">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
              </svg>
              {{ i18n.t ? i18n.t('download_cv') : 'Download CV' }}
            </button>
          </div>
        </div>
      </section>

    </article>
  </div>

  <div class="px-5 py-5 md:px-12 md:py-10 text-left text-amber-50 mx-3">
    <article data-page="about">
      <header>
        <div class="text-2xl font-bold text-black dark:text-white mb-5 fadein-bot title-section flex items-center">
          <div class="h-[1px] w-10 bg-blue-400 md:w-20 aos-init aos-animate" data-aos="zoom-in-left"
            data-aos-duration="600"></div>
          &nbsp; {{ i18n.t ? i18n.t('skills') : 'Skills' }}
        </div>
      </header>
      <section>
        <div>
          <ul class="flex flex-wrap text-sm font-medium text-center text-gray-500 dark:text-gray-400 mb-5">
            <li class="mr-2">
              <button class="inline-block px-4 py-3 rounded-lg hover:text-black dark:text-white dark:hover:text-white"
                :class="{ 'text-blue-400 bg-blue-400 bg-opacity-10': activeTab === 1 }" @click="activeTab = 1">{{ i18n.t ? i18n.t('tech_stack') : 'Tech Stack' }}</button>
            </li>
            <li class="mr-2">
              <button class="inline-block px-4 py-3 rounded-lg hover:text-black dark:text-white dark:hover:text-white"
                :class="{ 'text-blue-400 bg-blue-400 bg-opacity-10': activeTab === 2 }" @click="activeTab = 2">{{ i18n.t ? i18n.t('tools') : 'Tools' }}</button>
            </li>
          </ul>
        </div>
        <div v-show="activeTab === 1">
          <div class="grid grid-cols-2 gap-4 pb-32 md:grid-cols-3 md:gap-8 xl:grid-cols-4 xl:gap-10 2xl:gap-12">
            <div v-for="item in tech" :key="item.id">
              <div
                class="item-tech flex cursor-pointer items-center gap-2 rounded border border-blue-400 px-2 py-2 hover:bg-blue-400 hover:bg-opacity-10 md:gap-3 lg:px-3">
                <div class="flex h-12 w-12 items-center justify-center p-0 lg:h-16 lg:w-16 lg:p-2 zoom-in">
                  <img :alt="item.name" :src="item.imageUrl" class="img-tech drop-shadow-xl transition-all duration-300 h-[65%] w-[65%] lg:h-[85%] lg:w-[85%]" />
                </div>
                <div class="flex items-center text-sm md:text-base lg:text-lg">
                  <div class="tech font-medium text-black dark:text-white transition-all duration-300 translate-y-0 ">{{ item.name }}</div>
                  <div
                    class="status-tech opacity-0 absolute mt-5 text-[10px] text-blue-400 transition-all duration-300 md:text-xs lg:text-sm">
                    {{ i18n.t ? i18n.t(item.statusKey) : item.statusKey }}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div v-show="activeTab === 2">
          <div class="grid grid-cols-2 gap-4 pb-32 md:grid-cols-3 md:gap-8 xl:grid-cols-4 xl:gap-10 2xl:gap-12">
            <div v-for="item in tools" :key="item.id">
              <div
                class="item-tech flex cursor-pointer items-center gap-2 rounded border border-blue-400 px-2 py-2 hover:bg-blue-400 hover:bg-opacity-10 md:gap-3 lg:px-3">
                <div class="flex h-12 w-12 items-center justify-center p-0 lg:h-16 lg:w-16 lg:p-2 zoom-in">
                  <img :alt="item.name" :src="item.imageUrl" class="img-tech drop-shadow-xl transition-all duration-300 h-[65%] w-[65%] lg:h-[85%] lg:w-[85%]" />
                </div>
                <div class="flex items-center text-sm md:text-base lg:text-lg">
                  <div class="tech font-medium text-black dark:text-white transition-all duration-300 translate-y-0 ">{{ item.name }}</div>
                  <div
                    class="status-tech opacity-0 absolute mt-5 text-[10px] text-blue-400 transition-all duration-300 md:text-xs lg:text-sm">
                    {{ i18n.t ? i18n.t(item.statusKey) : item.statusKey }}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </article>
  </div>
</template>


<style>
.fadein-left {
  opacity: 0;
  animation: fadeInLeft 0.5s ease-out forwards;
}

@keyframes fadeInLeft {
  0% {
    opacity: 0;
    transform: translateX(100%);
  }

  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

.fadeins-1 {
  animation-delay: 500ms;
}

.fadeins-2 {
  animation-delay: 800ms;
}

.img-tech,
.tech {
  transition: transform 0.3s ease;
}

.item-tech:hover .img-tech {
  transform: scale(1.3);
}

.item-tech:hover .tech {
  transform: translateY(-12px);
}

.item-tech:hover .status-tech {
  opacity: 1;
}
</style>
