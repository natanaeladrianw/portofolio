<script>
export default {
  inject: ['i18n'],
  data() {
    return {
      activeTab: 1,
      isGalleryOpen: false,
      galleryImages: [],
      galleryTitle: '',
      currentImageIndex: 0,
      galleryMap: {
        2: [
          'program dilan 1.jpg',
          'program dilan 2.jpg',
          'program dilan 3.jpg',
          'program dilan 4.jpg',
          'program dilan 5.jpg'
        ]
      },
      items: [
        {
          id: 1,
          nameKey: 'personal_website_name',
          imageUrl: 'portofolio-web_personal',
          statusKey: 'personal_website_desc',
          tech: 'VueJS 3, Tailwind',
          github: 'https://github.com/natanaeladrianw/portofolio',
          demo: 'https://adrianwrwn.netlify.app/'
        },
        {
          id: 2,
          nameKey: 'cafe_system_name',
          imageUrl: 'logo dilan',
          statusKey: 'cafe_system_desc',
          tech: 'Laravel 10, Bootstrap, MySQL, JavaScript',
          github: 'https://github.com/natanaeladrianw/dindinglangit'
        }
      ]
    };
  },
  methods: {
    fallbackToJpg(event, base) {
      const img = event.target;
      if (img && !img.dataset.fallbackTried) {
        img.dataset.fallbackTried = 'true';
        img.src = `/img/${base}.jpg`;
      }
    },
    openGallery(item) {
      const images = this.galleryMap[item.id] || [];
      this.galleryImages = images.map((name) => `/img/dindinglangit/${encodeURIComponent(name)}`);
      this.galleryTitle = this.i18n.t ? this.i18n.t(item.nameKey) : item.nameKey;
      this.isGalleryOpen = true;
      this.currentImageIndex = 0;
      document.body.style.overflow = 'hidden';
    },
    closeGallery() {
      this.isGalleryOpen = false;
      this.galleryImages = [];
      this.galleryTitle = '';
      document.body.style.overflow = '';
    },
    showPrevImage() {
      if (!this.galleryImages.length) return;
      this.currentImageIndex = (this.currentImageIndex - 1 + this.galleryImages.length) % this.galleryImages.length;
    },
    showNextImage() {
      if (!this.galleryImages.length) return;
      this.currentImageIndex = (this.currentImageIndex + 1) % this.galleryImages.length;
    }
  }
}
</script>
<template>
  <div class="px-5 py-5 md:px-12 md:py-10 text-left text-black mx-3">
    <article data-page="about">
      <header>
        <div
          class="text-2xl font-bold text-black dark:text-white mb-10 fadein-bot title-section flex items-center justify-center flex-col">
          <h4>{{ i18n.t ? i18n.t('past_projects') : 'Past Project Experience' }}</h4>
          <h4 class="text-base font-normal text-transparent bg-clip-text bg-gradient-to-r from-blue-300 via-blue-500 to-blue-800">
            {{ i18n.t ? i18n.t('explore_projects') : "Explore the projects I've worked on so far" }}</h4>
        </div>
      </header>
      <section>
        <div>
          <div class="grid grid-cols-1 gap-4 pb-32 md:grid-cols-3 md:gap-3 xl:grid-cols-3 xl:gap-3 2xl:gap-5 fade-zoom-in">
            <div v-for="item in items" :key="item.id" class="h-full">
              <div
                class="item-card h-full flex flex-col items-center gap-2 rounded bg-white dark:bg-gray-800 hover:bg-gray-50 dark:hover:bg-gray-700 border border-blue-400 dark:border-blue-400 rounded-xl text-black dark:text-gray-100 md:gap-3 px-5 py-5 lg:px-5 shadow-sm hover:shadow-md transition-shadow ">
                <div class="flex items-center justify-center p-0 w-full lg:p-0 zoom-in">
                  <img :alt="i18n.t ? i18n.t(item.nameKey) : item.nameKey" loading="lazy" decoding="async" data-nimg="1" :class="['drop-shadow-xl rounded rounded-xl w-full h-48 object-contain', item.id === 2 ? 'dark:invert dark:brightness-200' : '']"
                    :src="'/img/' + item.imageUrl + '.png'" @error="fallbackToJpg($event, item.imageUrl)">
                </div>
                <div class="w-full flex-1 flex flex-col gap-2 items-center text-sm md:text-base lg:text-lg">
                  <div class="title-text font-medium text-blue-600 dark:text-blue-400">{{ i18n.t ? i18n.t(item.nameKey) : item.nameKey }}
                  </div>
                  <div class="w-full text-left text-[10px] text-gray-600 dark:text-gray-300 md:text-xs lg:text-sm">
                    {{ i18n.t ? i18n.t(item.statusKey) : item.statusKey }}</div>
                  <div class="w-full mt-4 text-normal text-sm text-left text-blue-600 dark:text-blue-400">
                    {{ item.tech }}
                  </div>
                  <div class="w-full mt-2 flex justify-start" v-if="galleryMap[item.id] && galleryMap[item.id].length">
                    <button @click="openGallery(item)" class="px-3 py-1 text-xs md:text-sm rounded bg-blue-600 text-white hover:bg-blue-700 transition-colors">{{ i18n.t ? i18n.t('view_gallery') : 'View' }}</button>
                  </div>
                  <div class="w-full flex justify-end mt-auto">
                    <div class="flex cursor-pointer items-end gap-2 text-primary">
                      <a v-if="item.github !== 'null'"
                        :href="item.github" target="_blank" rel="noreferrer"
                        title="View github repository" class="transition-all hover:text-blue-600">
                        <svg stroke="currentColor"
                          fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round"
                          height="16" width="16" xmlns="http://www.w3.org/2000/svg">
                          <path
                            d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22">
                          </path>
                        </svg></a>
                        <a v-if="item.id !== 2 && item.demo !== 'null'" :href="item.demo" target="_blank" rel="noreferrer"
                        title="View finished project" class="transition-all hover:text-blue-600">
                        <svg stroke="currentColor"
                          fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round"
                          height="18" width="18" xmlns="http://www.w3.org/2000/svg">
                          <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
                          <polyline points="15 3 21 3 21 9"></polyline>
                        <line x1="10" y1="14" x2="21" y2="3"></line>
                      </svg></a></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </article>
  
  <transition name="fade">
    <div v-if="isGalleryOpen" class="fixed inset-0 z-[9999] flex items-center justify-center">
      <div class="absolute inset-0 bg-black bg-opacity-80" @click="closeGallery"></div>
      <div class="relative bg-white dark:bg-gray-900 rounded-lg shadow-lg max-w-6xl w-[95vw] md:w-[90vw] p-4">
        <div class="flex items-center justify-between mb-3">
          <h3 class="text-lg md:text-xl font-semibold text-gray-800 dark:text-gray-100">{{ galleryTitle }} - {{ i18n.t ? i18n.t('gallery') : 'Gallery' }}</h3>
          <button @click="closeGallery" class="text-gray-500 hover:text-gray-700 dark:text-gray-300 dark:hover:text-gray-200">✕</button>
        </div>
        <div class="relative w-full flex items-center justify-center select-none">
          <button @click.stop="showPrevImage" class="absolute left-0 md:left-2 top-1/2 -translate-y-1/2 bg-blue-600 text-white rounded-full w-10 h-10 md:w-12 md:h-12 text-xl flex items-center justify-center hover:bg-blue-700">‹</button>
          <img :src="galleryImages[currentImageIndex]" class="max-h-[80vh] md:max-h-[85vh] w-auto rounded shadow-sm" :alt="galleryTitle + ' image ' + (currentImageIndex+1)">
          <button @click.stop="showNextImage" class="absolute right-0 md:right-2 top-1/2 -translate-y-1/2 bg-blue-600 text-white rounded-full w-10 h-10 md:w-12 md:h-12 text-xl flex items-center justify-center hover:bg-blue-700">›</button>
        </div>
        <div class="mt-3 text-center text-sm text-gray-600">{{ currentImageIndex + 1 }} / {{ galleryImages.length }}</div>
      </div>
    </div>
  </transition>

</div></template>

<style>
.item-card:hover {
  transition: transform 0.3s ease;
  transform: translateY(-8px);
}
svg:hover{
  stroke: #2563eb;
}
@keyframes fadeZoomIn {
  0% {
    opacity: 0;
    transform: scale(0.5);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

/* Menggunakan animasi pada elemen yang diinginkan */
.fade-zoom-in {
  animation: fadeZoomIn 1s ease-in-out;
}
</style>