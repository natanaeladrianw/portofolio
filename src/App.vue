<template>
  <!-- component -->
  <!-- This is an example component -->
  <div class="max-w-7xl mx-auto flex flex-col relative">

    <nav class="max-w-7xl px-5 md:fixed top-0 z-[98] w-screen backdrop-blur-md dark:backdrop-blur-0 bg-white dark:bg-[#0f172a] bg-opacity-90 dark:bg-opacity-100 border-b-0 border-transparent shadow-none">
      <div class="container mx-auto flex flex-wrap items-center justify-between">
        <button @click="redirectToHome" class="flex">
          <span class="self-center text-lg text-blue-500 dark:text-blue-400 font-semibold whitespace-nowrap fadein-bot hover:text-blue-600 dark:hover:text-blue-300">adrianWirawan();</span>
        </button>
        <div class="flex md:order-2 fadein-bot gap-4 items-center">
          <button @click="toggleTheme" :title="isDark ? 'Switch to light' : 'Switch to dark'"
                  class="w-9 h-9 flex items-center justify-center rounded-full border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-800 text-gray-700 dark:text-gray-200 shadow-sm hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors">
            <svg v-if="!isDark" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="w-5 h-5 text-yellow-400" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M9 18h6"/>
              <path d="M10 22h4"/>
              <path d="M8 14a4 4 0 1 1 8 0c0 1.657-1 2.5-1.5 3H9.5C9 16.5 8 15.657 8 14z"/>
              <path d="M12 2v2M4.93 4.93l1.41 1.41M2 12h2M19.07 4.93l-1.41 1.41M20 12h2M6 20l1.5-1.5M18 20l-1.5-1.5"/>
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="w-5 h-5 text-gray-200" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M9 18h6"/>
              <path d="M10 22h4"/>
              <path d="M8 14a4 4 0 1 1 8 0c0 1.657-1 2.5-1.5 3H9.5C9 16.5 8 15.657 8 14z"/>
            </svg>
          </button>
          <div class="relative">
            <button @click="showLangMenu = !showLangMenu" class="w-9 h-9 flex items-center justify-center rounded-full border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-800 text-gray-700 dark:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors" :title="currentLang.toUpperCase()">
              <span class="text-xs font-semibold">{{ currentLang.toUpperCase() }}</span>
            </button>
            <div v-if="showLangMenu" class="absolute right-0 top-11 bg-white dark:bg-gray-800 rounded-md shadow-md border border-gray-200 dark:border-gray-700 overflow-hidden">
              <button @click="setLang('en')" class="block px-4 py-2 text-sm w-full text-left hover:bg-gray-100 dark:hover:bg-gray-700" :class="{ 'font-semibold text-blue-600': currentLang==='en' }">English</button>
              <button @click="setLang('id')" class="block px-4 py-2 text-sm w-full text-left hover:bg-gray-100 dark:hover:bg-gray-700" :class="{ 'font-semibold text-blue-600': currentLang==='id' }">Indonesia</button>
            </div>
          </div>
          <a href="https://github.com/natanaeladrianw" target="_blank" rel="noopener noreferrer" class="w-9 h-9 flex items-center justify-center rounded-full border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-800 text-gray-700 dark:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors" aria-label="GitHub">
            <svg viewBox="0 0 24 24" class="w-5 h-5" fill="currentColor" aria-hidden="true">
              <path d="M12 2C6.475 2 2 6.486 2 12.021c0 4.431 2.865 8.19 6.839 9.51.5.092.683-.217.683-.482 0-.237-.009-.866-.013-1.7-2.782.604-3.368-1.343-3.368-1.343-.454-1.155-1.11-1.463-1.11-1.463-.908-.62.069-.607.069-.607 1.004.071 1.532 1.032 1.532 1.032.892 1.53 2.341 1.088 2.91.833.091-.647.35-1.088.636-1.338-2.221-.253-4.556-1.112-4.556-4.947 0-1.092.39-1.987 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.269 2.75 1.026A9.564 9.564 0 0 1 12 6.844c.851.004 1.707.116 2.507.341 1.909-1.295 2.748-1.026 2.748-1.026.545 1.378.202 2.397.099 2.65.64.701 1.028 1.596 1.028 2.688 0 3.845-2.339 4.691-4.566 4.94.359.309.678.919.678 1.852 0 1.337-.012 2.418-.012 2.747 0 .267.18.579.688.48A10.026 10.026 0 0 0 22 12.02C22 6.486 17.523 2 12 2z"/>
            </svg>
          </a>
          <a href="https://www.linkedin.com/in/nathanaeladrianwirawan/" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn"
             class="w-9 h-9 flex items-center justify-center rounded-full border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-800 text-[#0a66c2] dark:text-[#60a5fa] hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors">
            <svg viewBox="0 0 24 24" class="w-5 h-5" fill="currentColor" aria-hidden="true">
              <path d="M19 3A2.94 2.94 0 0 1 22 6v12a2.94 2.94 0 0 1-3 3H5a2.94 2.94 0 0 1-3-3V6a2.94 2.94 0 0 1 3-3Zm-9.6 7H6.4V18h3V10Zm-1.5-1.8a1.74 1.74 0 1 0 0-3.48 1.74 1.74 0 0 0 0 3.48ZM20 18v-4.8c0-2.58-1.38-3.78-3.22-3.78a2.78 2.78 0 0 0-2.53 1.4h-.06V10H11v8h3v-4.46c0-1.18.22-2.33 1.69-2.33 1.44 0 1.46 1.34 1.46 2.4V18Z"/>
            </svg>
          </a>
        </div>

        <div class="hidden md:flex items-center ml-4 relative"></div>
        <div class="hidden md:flex flex-1 justify-center items-center md:order-1" id="mobile-menu-3">
          <ul class="flex-col md:flex-row flex md:space-x-8 mt-4 md:mt-0 md:text-sm md:font-medium">
            <li>
              <router-link to="/"
                class="fadein-bot text-navy-600 dark:text-gray-200 hover:bg-blue-50 dark:hover:bg-gray-800 border-b border-gray-100 dark:border-gray-800 md:hover:bg-transparent md:border-0 block pl-3 pr-4 py-2 md:hover:text-navy-700 md:p-0"
                aria-current="page">{{ t('home') }}</router-link>
            </li>
            <li>
              <router-link to="/about"
                class="fadein-bot fadein-1 text-navy-600 dark:text-gray-200 hover:bg-blue-50 dark:hover:bg-gray-800 border-b border-gray-100 dark:border-gray-800 md:hover:bg-transparent md:border-0 block pl-3 pr-4 py-2 md:hover:text-navy-700 md:p-0">{{ t('about') }}</router-link>
            </li>
            <li>
              <router-link to="/portfolio"
                class="fadein-bot fadein-2 text-navy-600 dark:text-gray-200 hover:bg-blue-50 dark:hover:bg-gray-800 border-b border-gray-100 dark:border-gray-800 md:hover:bg-transparent md:border-0 block pl-3 pr-4 py-2 md:hover:text-navy-700 md:p-0">{{ t('portfolio') }}</router-link>
            </li>
            <li>
              <router-link to="/certificate"
                class="fadein-bot fadein-3 text-navy-600 dark:text-gray-200 hover:bg-blue-50 dark:hover:bg-gray-800 border-b border-gray-100 dark:border-gray-800 md:hover:bg-transparent md:border-0 block pl-3 pr-4 py-2 md:hover:text-navy-700 md:p-0 blog">{{ t('certificate') }}</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div class="md:mt-[100px]">
      <router-view />
    </div>
  </div>
  <footer class="block md:hidden fixed bottom-0 left-0 right-0 rounded-t-3xl border border-gray-300 dark:border-gray-700 bg-gray-200 dark:bg-gray-900 bg-opacity-70 dark:bg-opacity-80 backdrop-blur-md backdrop-opacity-90 shadow-lg">
  <nav class="flex justify-around py-4 text-xs text-gray-800 dark:text-gray-200">
    <router-link to="/" class="text-navy-600 dark:text-gray-200 hover:text-navy-700 dark:hover:text-white">Home</router-link>
    <router-link to="/about" class="text-navy-600 dark:text-gray-200 hover:text-navy-700 dark:hover:text-white">About</router-link>
    <router-link to="/portfolio" class="text-navy-600 dark:text-gray-200 hover:text-navy-700 dark:hover:text-white">Portfolio</router-link>
    <router-link to="/certificate" class="text-navy-600 dark:text-gray-200 hover:text-navy-700 dark:hover:text-white">Certificate</router-link>
  </nav>
</footer>
</template>

<script>
export default {
  data() {
    return {
      isDark: false,
      currentLang: 'en',
      showLangMenu: false,
      translations: {
        en: {
          home: 'Home',
          about: 'About',
          portfolio: 'Portfolio',
          certificate: 'Certificate',
          about_me: 'About Me',
          tech_stack: 'Tech Stack',
          tools: 'Tools',
          past_projects: 'Past Project Experience',
          explore_projects: "Explore the projects I've worked on so far",
          certificates_awards: 'Certificates and Awards',
          sidebar_cert_ach: 'Certificates and Achievements',
          skills: 'Skills',
          hello_world_im: "Hello World, I'm",
          welcome: 'Welcome to My personal website.',
          tech_enthusiast: 'Tech Enthusiast',
          web_developer: 'Web Developer',
          full_stack_engineer: 'Full-stack Engineer',
          informatics_student: 'Informatics Student',
          about_me_paragraph1: 'Hi everyone! My name is Nathanael Adrian Wirawan. I am a web and mobile developer with experience in building applications using technologies such as HTML, CSS, JavaScript, PHP, Laravel, Vue.js, Python, Kotlin, and Java. I am passionate about creating digital solutions that are not only functional but also efficient and visually appealing. For me, programming is not just a skill, but also a form of creativity that brings ideas to life.',
          about_me_paragraph2: 'My focus is to develop applications and websites that are user-friendly, responsive, and tailored to the client\'s needs. I also pay attention to design and usability, ensuring that every project delivers both value and satisfaction. My goal is to help businesses and individuals convey their message effectively through technology. If you are interested in collaborating with me, please feel free to reach out through the contact listed.',
          advanced: 'Advanced',
          intermediate: 'Intermediate',
          beginner: 'Beginner',
          version_control: 'Version Control',
          git_hosting: 'Git Hosting',
          package_manager: 'Package Manager',
          database: 'Database',
          personal_website_name: 'Personal Website',
          personal_website_desc: 'This personal website serves as a platform to showcase my profile, skills, and projects, as well as a space for me to explore and experiment with new technologies.',
          cafe_system_name: 'Sky Wall Cafe Inventory Information System',
          cafe_system_desc: 'A web-based system for managing warehouse and kitchen stock, equipped with POS features and WMA-based raw material prediction to support efficient café operations.',
          view_gallery: 'View',
          gallery: 'Gallery',
          certificate_collection_desc: 'A collection of internship certificates, training, and awards that I have received.',
          category: 'Category',
          all: 'All',
          internship: 'Internship',
          training: 'Training',
          certification: 'Certification',
          statistics: 'Statistics',
          total_certificates: 'Total Certificates',
          issuer: 'Issuer',
          duration: 'Duration',
          view_certificate: 'View Certificate',
          download_cv: 'Download CV',
          laravel_cert_title: 'Laravel Staff Internship Certificate',
          laravel_cert_desc: 'Internship at Lokpro Media as a Laravel Staff with a focus on developing web applications using the Laravel framework and modern backend technologies.',
          laravel_cert_date: 'September - December 2024',
          laravel_cert_category: 'Internship'
        },
        id: {
          home: 'Beranda',
          about: 'Tentang',
          portfolio: 'Portofolio',
          certificate: 'Sertifikat',
          about_me: 'Tentang Saya',
          tech_stack: 'Tumpukan Teknologi',
          tools: 'Alat',
          past_projects: 'Pengalaman Proyek',
          explore_projects: 'Jelajahi proyek yang telah saya kerjakan sejauh ini',
          certificates_awards: 'Sertifikat dan Penghargaan',
          sidebar_cert_ach: 'Sertifikat dan Pencapaian',
          skills: 'Keahlian',
          hello_world_im: "Halo Dunia, saya",
          welcome: 'Selamat datang di website pribadi saya.',
          tech_enthusiast: 'Penggemar Teknologi',
          web_developer: 'Pengembang Web',
          full_stack_engineer: 'Engineer Full‑stack',
          informatics_student: 'Mahasiswa Informatika',
          about_me_paragraph1: 'Halo semuanya! Nama saya Nathanael Adrian Wirawan. Saya adalah seorang pengembang web dan mobile dengan pengalaman dalam membangun aplikasi menggunakan teknologi seperti HTML, CSS, JavaScript, PHP, Laravel, Vue.js, Python, Kotlin, dan Java. Saya sangat antusias dalam menciptakan solusi digital yang tidak hanya fungsional tetapi juga efisien dan menarik secara visual. Bagi saya, pemrograman bukan hanya sebuah keterampilan, tetapi juga bentuk kreativitas yang menghidupkan ide-ide.',
          about_me_paragraph2: 'Fokus saya adalah mengembangkan aplikasi dan website yang ramah pengguna, responsif, dan disesuaikan dengan kebutuhan klien. Saya juga memperhatikan desain dan kegunaan, memastikan bahwa setiap proyek memberikan nilai dan kepuasan. Tujuan saya adalah membantu bisnis dan individu menyampaikan pesan mereka secara efektif melalui teknologi. Jika Anda tertarik untuk berkolaborasi dengan saya, silakan hubungi melalui kontak yang tertera.',
          advanced: 'Mahir',
          intermediate: 'Menengah',
          beginner: 'Pemula',
          version_control: 'Kontrol Versi',
          git_hosting: 'Hosting Git',
          package_manager: 'Manajer Paket',
          database: 'Basis Data',
          personal_website_name: 'Website Pribadi',
          personal_website_desc: 'Website pribadi ini berfungsi sebagai platform untuk menampilkan profil, keahlian, dan proyek saya, serta sebagai ruang untuk saya menjelajahi dan bereksperimen dengan teknologi baru.',
          cafe_system_name: 'Sistem Informasi Inventori Kafe Dinding Langit',
          cafe_system_desc: 'Sistem berbasis web untuk mengelola stok gudang dan dapur, dilengkapi dengan fitur POS dan prediksi bahan baku berbasis WMA untuk mendukung operasional kafe yang efisien.',
          view_gallery: 'Lihat',
          gallery: 'Galeri',
          certificate_collection_desc: 'Kumpulan sertifikat magang, pelatihan, dan penghargaan yang telah saya terima.',
          category: 'Kategori',
          all: 'Semua',
          internship: 'Magang',
          training: 'Pelatihan',
          certification: 'Sertifikasi',
          statistics: 'Statistik',
          total_certificates: 'Total Sertifikat',
          issuer: 'Penerbit',
          duration: 'Durasi',
          view_certificate: 'Lihat Sertifikat',
          download_cv: 'Unduh CV',
          laravel_cert_title: 'Sertifikat Magang Staff Laravel',
          laravel_cert_desc: 'Magang di Lokpro Media sebagai Staff Laravel dengan fokus mengembangkan aplikasi web menggunakan framework Laravel dan teknologi backend modern.',
          laravel_cert_date: 'September - Desember 2024',
          laravel_cert_category: 'Magang'
        }
      }
    }
  },
  provide() {
    return {
      i18n: this
    }
  },
  methods: {
    t(key) {
      return (this.translations[this.currentLang] && this.translations[this.currentLang][key]) || key
    },
    redirectToHome() {
      this.$router.push('/')
    },
    toggleTheme() {
      this.isDark = !this.isDark
      const root = document.documentElement
      if (this.isDark) {
        root.classList.add('dark')
        localStorage.setItem('theme', 'dark')
      } else {
        root.classList.remove('dark')
        localStorage.setItem('theme', 'light')
      }
    },
    setLang(lang) {
      this.currentLang = lang
      localStorage.setItem('lang', lang)
      this.showLangMenu = false
    }
  },
  mounted() {
    const saved = localStorage.getItem('theme')
    const prefersDark = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches
    this.isDark = saved ? saved === 'dark' : prefersDark
    const root = document.documentElement
    if (this.isDark) root.classList.add('dark')

    const savedLang = localStorage.getItem('lang')
    this.currentLang = savedLang === 'id' ? 'id' : 'en'
  }
}
</script>

<style>
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

::-webkit-scrollbar {
  width: 5px; /* for vertical scrollbar */
  height: 5px; /* for horizontal scrollbar */
}

::-webkit-scrollbar-track {
  background: #f3f4f6;
  border-radius: 5px;
}

::-webkit-scrollbar-thumb {
  background: #1e3a8a;
  border-radius: 5px;
}

::-webkit-scrollbar-button { width: 20px; }

body {
  font-family: 'Poppins', sans-serif;
  background: white;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}

.dark body {
  background: #0f172a;
  color: #e5e7eb;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  transition: color 0.3s;
}

nav a.router-link-exact-active {
  display: inline-flex;
  flex-direction: column;
  color: #1e3a8a;
  transition: color 0.3s;
}

nav a.router-link-exact-active::after {
  display: inline-block;
  content: "";
  margin-top: 0.08em;
  width: 100%;
  height: 4px;
  border-radius: 2px;
  background-color: #1e3a8a;
}

nav a.router-link-exact-active:hover {
  color: #1e3a8a;
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

</style>
