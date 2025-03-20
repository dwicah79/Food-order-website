<template>
  <div class="flex flex-wrap w-full px-20">
    <div class="w-1/2">
      <div class="flex justify-center items-center h-full">
        <div class="flex flex-col px-10">
          <h1 class="font-bold text-lg md:text-4xl">
            Menu Makanan yang Lezat, Selalu tersedia di sistem kami
          </h1>
          <h1>Ayo segera pilih dan pesan menu kesukaan anda !!!</h1>
          <router-link
            to="/menu"
            class="bg-green-400 hover:bg-green-500 rounded-lg px-5 py-2 w-fit"
          >
            <font-awesome-icon :icon="['fab', 'whatsapp']" />
            Pesan Sekarang</router-link
          >
        </div>
      </div>
    </div>
    <div class="w-1/2">
      <div class="flex justify-center items-center">
        <img src="../assets/image/ilustrasi.png" alt="logo makan" class="p-5 w-full" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {
    return {}
  },
}
</script>

<style lang="scss" scoped></style>
