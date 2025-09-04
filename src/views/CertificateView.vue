<template>
  <div class="px-5 py-5 md:px-12 md:py-10 text-left text-black dark:text-white mx-3">
    <article data-page="certificate">
      <header>
        <div class="text-2xl font-bold text-black dark:text-white mb-10 fadein-bot title-section flex items-center justify-center flex-col">
          <h4>{{ i18n.t ? i18n.t('certificates_awards') : 'Certificates and Awards' }}</h4>
          <h4 class="text-base font-normal text-transparent bg-clip-text bg-gradient-to-r from-blue-300 via-blue-500 to-blue-800">
            {{ i18n.t ? i18n.t('certificate_collection_desc') : 'A collection of internship certificates, training, and awards that I have received.' }}</h4>
        </div>
      </header>
      
      <section>
        <div class="flex flex-col-reverse md:flex-row relative">
          <div class="w-full md:w-2/3">
            <div class="grid grid-cols-1 gap-4 pb-32 md:grid-cols-1 md:gap-3 xl:grid-cols-1 xl:gap-3 2xl:gap-5 fade-zoom-in">
          <div v-for="certificate in filteredCertificates" :key="certificate.id" 
               class="item-card flex flex-col items-center gap-2 rounded bg-white dark:bg-gray-800 hover:bg-gray-50 dark:hover:bg-gray-700 border border-blue-400 dark:border-blue-400 rounded-xl text-black dark:text-gray-100 md:gap-3 px-5 py-5 lg:px-5">
            <div class="flex flex-col md:flex-row items-start gap-4 md:gap-6 w-full">
              <div class="w-full md:w-2/3">
                <div class="flex items-center gap-2 mb-3">
                  <div class="h-[1px] w-16 bg-blue-400 md:w-8 aos-init aos-animate mr-2"></div>
                  <span class="text-xs text-gray-600 dark:text-white italic">{{ i18n.t ? i18n.t(certificate.dateKey) : certificate.dateKey }}</span>
                  <span class="px-3 py-1 rounded-full text-xs font-medium" 
                        :class="getCategoryClass(i18n.t ? i18n.t(certificate.categoryKey) : certificate.categoryKey)">
                    {{ i18n.t ? i18n.t(certificate.categoryKey) : certificate.categoryKey }}
                  </span>
                </div>
                <div class="title-text font-medium text-blue-600 text-sm md:text-base lg:text-lg mb-2">{{ i18n.t ? i18n.t(certificate.titleKey) : certificate.titleKey }}</div>
                <div class="w-full text-left text-[10px] text-gray-600 dark:text-white md:text-xs lg:text-sm mb-3">{{ i18n.t ? i18n.t(certificate.descriptionKey) : certificate.descriptionKey }}</div>
                <div class="flex flex-wrap gap-2 mb-3">
                  <span v-for="skill in certificate.skills" :key="skill" 
                        class="px-3 py-1 rounded-full bg-blue-100 text-blue-600 text-xs">
                    {{ skill }}
                  </span>
                </div>
                <div class="w-full text-left text-[10px] text-gray-600 dark:text-white md:text-xs lg:text-sm">
                  <p><strong>{{ i18n.t ? i18n.t('issuer') : 'Issuer' }}:</strong> {{ certificate.issuer }}</p>
                  <p v-if="certificate.duration"><strong>{{ i18n.t ? i18n.t('duration') : 'Duration' }}:</strong> {{ certificate.duration }}</p>
                </div>
                <div v-if="certificate.image" class="mt-3">
                  <button @click="viewCertificate(certificate)" 
                          class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors duration-200 text-xs font-medium">
                    👁️ {{ i18n.t ? i18n.t('view_certificate') : 'View Certificate' }}
                  </button>
                </div>
              </div>
              <div class="w-full md:w-1/3 flex justify-center">
                <div class="flex h-12 w-12 items-center justify-center p-0 h-full w-full lg:p-0 zoom-in">
                  <img :src="'/img/' + certificate.image" :alt="i18n.t ? i18n.t(certificate.titleKey) : certificate.titleKey" 
                       class="drop-shadow-xl rounded rounded-xl w-full h-full object-cover">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="w-full md:w-1/3 h-fit p-4 md:p-8 md:sticky md:top-24">
        <!-- Sidebar -->
        <div class="flex flex-col text-left">
          <div class="bg-clip-text bg-gradient-to-r from-blue-300 via-blue-500 to-blue-800 text-transparent text-lg font-semibold">
            {{ i18n.t ? i18n.t('sidebar_cert_ach') : 'Certificates and Achievements' }}
          </div>
          <div class="h-[1px] mt-7 mb-7 w-20 bg-blue-400 aos-init aos-animate mr-2"></div>
          
          <div class="block">
            <div class="text-black dark:text-white text-md font-semibold mb-3">{{ i18n.t ? i18n.t('category') : 'Category' }}</div>
            <div class="flex flex-wrap gap-2 mb-6">
              <span v-for="category in categories" :key="category.name"
                    :class="[
                      'py-2 px-3 rounded-2xl text-xs cursor-pointer transition-colors',
                      activeFilter === category.name 
                        ? 'bg-blue-500 text-white font-semibold' 
                        : 'bg-gray-100 hover:bg-blue-100 text-gray-700'
                    ]"
                    @click="filterByCategory(category.originalName)">
                {{ i18n.t ? i18n.t(category.nameKey) : category.name }}
              </span>
            </div>
            
            <div class="text-black dark:text-white text-md font-semibold mb-3">{{ i18n.t ? i18n.t('statistics') : 'Statistics' }}</div>
            <div class="space-y-2 text-sm text-gray-600 dark:text-white">
              <div class="flex justify-between">
                <span>{{ i18n.t ? i18n.t('total_certificates') : 'Total Certificates' }}:</span>
                <span class="text-blue-600 font-semibold">{{ filteredCertificates.length }}</span>
              </div>
              <div class="flex justify-between">
                <span>{{ i18n.t ? i18n.t('internship') : 'Internship' }}:</span>
                <span class="text-blue-600 font-semibold">{{ getCategoryCount('Internship') }}</span>
              </div>
              <div class="flex justify-between">
                <span>{{ i18n.t ? i18n.t('training') : 'Training' }}:</span>
                <span class="text-blue-600 font-semibold">{{ getCategoryCount('Training') }}</span>
              </div>
              <div class="flex justify-between">
                <span>{{ i18n.t ? i18n.t('certification') : 'Certification' }}:</span>
                <span class="text-blue-600 font-semibold">{{ getCategoryCount('Certification') }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</article>

  <!-- Modal untuk menampilkan sertifikat -->
  <div v-if="selectedCertificate" 
       class="fixed inset-0 flex items-center justify-center z-[9999] p-4 modal-overlay bg-gray-200 bg-opacity-60 dark:bg-black dark:bg-opacity-80"
       @click="closeModal">
    <div class="relative max-w-4xl w-full max-h-full modal-content">
      <div class="bg-white dark:bg-[#1e1e1f] rounded-xl p-6 relative">
        <!-- Header Modal -->
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-xl font-bold text-blue-600 dark:text-white">{{ i18n.t ? i18n.t(selectedCertificate.titleKey) : selectedCertificate.titleKey }}</h3>
          <button @click="closeModal" 
                  class="text-gray-400 hover:text-white text-2xl font-bold transition-colors">
            ×
          </button>
        </div>
        
        <!-- Gambar Sertifikat -->
        <div class="flex justify-center">
          <img :src="'/img/' + selectedCertificate.image" 
               :alt="i18n.t ? i18n.t(selectedCertificate.titleKey) : selectedCertificate.titleKey"
               class="max-w-full max-h-[70vh] object-contain rounded-lg shadow-2xl">
        </div>
        
        <!-- Footer Modal -->
        <div class="mt-4 text-center">
          <p class="text-blue-600 dark:text-gray-300 text-sm">
            {{ selectedCertificate.issuer }} • {{ i18n.t ? i18n.t(selectedCertificate.dateKey) : selectedCertificate.dateKey }}
          </p>
        </div>
      </div>
    </div>
  </div>
</div>
</template>
  
<script>
export default {
  inject: ['i18n'],
  data() {
    return {
      certificates: [
        {
          id: 1,
          titleKey: "laravel_cert_title",
          descriptionKey: "laravel_cert_desc",
          dateKey: "laravel_cert_date",
          categoryKey: "laravel_cert_category",
          issuer: "LOKPRO MEDIA",
          duration: "4 Months",
          skills: ["Laravel", "PHP", "MySQL", "Web Development"],
          image: "certificate-magang_lokpro.jpg"
        }
      ],
      categories: [
        { name: "All", nameKey: "all", originalName: "All", count: 0 },
        { name: "Internship", nameKey: "internship", originalName: "Internship", count: 0 },
        { name: "Training", nameKey: "training", originalName: "Training", count: 0 },
        { name: "Certification", nameKey: "certification", originalName: "Certification", count: 0 }
      ],
      selectedCertificate: null,
      activeFilter: "All"
    }
  },
  mounted() {
    this.updateCategoryCounts();
  },
  computed: {
    filteredCertificates() {
      if (this.activeFilter === "All") {
        return this.certificates;
      }
      return this.certificates.filter(cert => {
        // Compare with the original category name, not the translated one
        const originalCategoryName = this.getOriginalCategoryName(cert.categoryKey);
        return originalCategoryName === this.activeFilter;
      });
    }
  },
  methods: {
    getOriginalCategoryName(categoryKey) {
      const categoryMap = {
        'laravel_cert_category': 'Internship',
        'internship': 'Internship',
        'training': 'Training',
        'certification': 'Certification'
      };
      return categoryMap[categoryKey] || categoryKey;
    },
    getCategoryClass(category) {
      const classes = {
        'Internship': 'bg-blue-500/20 text-blue-300 border border-blue-500/30',
        'Magang': 'bg-blue-500/20 text-blue-300 border border-blue-500/30',
        'Training': 'bg-green-500/20 text-green-300 border border-green-500/30',
        'Pelatihan': 'bg-green-500/20 text-green-300 border border-green-500/30',
        'Certification': 'bg-purple-500/20 text-purple-300 border border-purple-500/30',
        'Sertifikasi': 'bg-purple-500/20 text-purple-300 border border-purple-500/30'
      };
      return classes[category] || 'bg-gray-500/20 text-gray-300 border border-gray-500/30';
    },
    getCategoryCount(categoryName) {
      return this.certificates.filter(cert => {
        const originalCategoryName = this.getOriginalCategoryName(cert.categoryKey);
        return originalCategoryName === categoryName;
      }).length;
    },
    updateCategoryCounts() {
      this.categories.forEach(category => {
        if (category.name === 'All') {
          category.count = this.certificates.length;
        } else {
          category.count = this.getCategoryCount(category.originalName);
        }
      });
    },
    filterByCategory(categoryName) {
      this.activeFilter = categoryName;
    },
    viewCertificate(certificate) {
      this.selectedCertificate = certificate;
    },
    closeModal() {
      this.selectedCertificate = null;
    }
  }
}
</script>

<style scoped>
.paraf {
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  text-overflow: ellipsis;
  overflow: hidden;
}

@media (min-width: 768px) { 
  .paraf {
    display: -webkit-box;
  }
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

.fade-zoom-in {
  animation: fadeZoomIn 1s ease-in-out;
}

/* Hover effects */
.item-card:hover {
  transition: transform 0.3s ease;
  transform: translateY(-8px);
}



/* Zoom in animation for images */
.zoom-in {
  transition: transform 0.3s ease;
}

.zoom-in:hover {
  transform: scale(1.05);
}

/* Modal animations */
.modal-enter-active, .modal-leave-active {
  transition: opacity 0.3s ease;
}

.modal-enter-from, .modal-leave-to {
  opacity: 0;
}

/* Prevent body scroll when modal is open */
body.modal-open {
  overflow: hidden;
}

/* Modal z-index fix */
.modal-overlay {
  z-index: 9999 !important;
}

.modal-content {
  z-index: 10000 !important;
}
</style>