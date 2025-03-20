<template>
  <div
    class="rounded-lg bg-white p-10 shadow-md transition-all duration-300 hover:shadow-lg hover:scale-105"
  >
    <!-- Gambar Produk -->
    <div class="relative">
      <!-- Skeleton Loading saat gambar belum dimuat -->
      <div v-if="!imageLoaded" class="w-full h-48 bg-gray-200 rounded-md animate-pulse"></div>
      <img
        :src="getImageUrl(product.gambar)"
        class="card-img-top w-full rounded-md"
        :class="{ 'opacity-0': !imageLoaded }"
        alt="Product Image"
        @load="imageLoaded = true"
      />
      <span
        class="absolute top-2 left-2 rounded-full px-2 py-1 text-xs font-semibold text-white"
        :class="product.is_ready ? 'bg-green-500' : 'bg-red-500'"
      >
        {{ product.is_ready ? 'Tersedia' : 'Habis' }}
      </span>
    </div>

    <!-- Konten Produk -->
    <div class="mt-3">
      <h3 class="text-lg font-semibold">{{ product.nama }}</h3>
      <p class="text-gray-500 text-sm">{{ product.kode }}</p>
      <p class="mt-1 text-lg font-bold text-green-600">{{ formatHarga(product.harga) }}</p>

      <!-- Tombol Add to Cart -->
      <button
        class="mt-3 w-full rounded-md px-4 py-2 font-semibold text-white transition duration-200"
        :class="
          product.is_ready
            ? 'bg-green-500 hover:bg-green-600 active:bg-green-700'
            : 'bg-gray-400 cursor-not-allowed'
        "
        :disabled="!product.is_ready"
        @click="addToCart"
      >
        {{ buttonText }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardProductComponent',
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      imageLoaded: false,
      buttonText: 'Add to Cart',
      isAdding: false,
    }
  },
  methods: {
    formatHarga(value) {
      return new Intl.NumberFormat('id-ID', {
        style: 'currency',
        currency: 'IDR',
      }).format(value)
    },
    getImageUrl(imageName) {
      // console.log(`Mencoba memuat gambar: ${imageName}`)
      try {
        const imageUrl = new URL(`/src/assets/image/${imageName}`, import.meta.url).href
        // console.log(`Gambar ditemukan: ${imageUrl}`)
        return imageUrl
      } catch (e) {
        console.error(`Gambar ${imageName} tidak ditemukan.`)
        return require('@/assets/image/fallback.jpg') // Gambar fallback
      }
    },
    addToCart() {
      if (this.isAdding || !this.product.is_ready) return

      this.isAdding = true
      this.buttonText = 'Menambahkan...'

      // Simulasi proses async (misalnya, API call)
      setTimeout(() => {
        this.isAdding = false
        this.buttonText = 'Ditambahkan!'
        setTimeout(() => {
          this.buttonText = 'Add to Cart'
        }, 2000) // Kembalikan teks tombol setelah 2 detik
      }, 1000) // Simulasi proses selama 1 detik
    },
  },
}
</script>

<style scoped>
/* Animasi untuk tombol */
button:active {
  transform: scale(0.95);
}

/* Transisi untuk gambar */
img {
  transition: opacity 0.3s ease;
}
</style>
