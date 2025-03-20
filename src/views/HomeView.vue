<script>
import TheWelcome from '../components/TheWelcome.vue'
import NavbarComponent from '@/components/NavbarComponent.vue'
import Hero from '@/components/Hero.vue'
import CardProductComponent from '@/components/CardProductComponent.vue'
import axios from 'axios'

export default {
  components: {
    TheWelcome,
    NavbarComponent,
    Hero,
    CardProductComponent,
  },
  data() {
    return {
      products: [],
      isLoading: true,
    }
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await axios.get('http://localhost:3000/best-products')
        this.products = response.data
        // console.log('Berhasil fetch data:', response.data)
      } catch (error) {
        console.error('Error fetching products:', error)
      } finally {
        this.isLoading = false
      }
    },
  },
  mounted() {
    this.fetchProducts()
  },
}
</script>

<template>
  <Hero />
  <h1 class="text-center font-bold text-lg md:text-4xl mb-6">BEST SELLER PRODUCTS</h1>

  <div class="flex justify-center mx-20">
    <div v-if="isLoading" class="text-center py-10 text-gray-500">Loading...</div>
    <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <CardProductComponent v-for="product in products" :key="product.id" :product="product" />
    </div>
  </div>
</template>
