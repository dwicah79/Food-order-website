<template>
  <div class="navbar bg-base-100 shadow-sm md:px-10">
    <div class="navbar-start">
      <div class="dropdown">
        <button @click="toggleDropdown" class="btn btn-ghost lg:hidden">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h8m-8 6h16"
            />
          </svg>
        </button>
        <ul
          v-if="dropdownOpen"
          class="menu menu-sm dropdown-content bg-base-100 rounded-box z-10 mt-3 w-52 p-2 shadow"
        >
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/menu">Menu Makanan</router-link></li>
        </ul>
      </div>
      <router-link to="/" class="btn btn-ghost text-xl">Food Order</router-link>
    </div>

    <div class="navbar-center hidden lg:flex">
      <ul class="menu menu-horizontal px-1">
        <li><router-link to="/">Home</router-link></li>
        <li><router-link to="/menu">Menu Makanan</router-link></li>
      </ul>
    </div>

    <div class="navbar-end">
      <button @click="togleclick" class="relative btn btn-ghost">
        <font-awesome-icon :icon="['fas', 'cart-shopping']" class="text-xl" />
        <span
          v-if="cartItemCount > 0"
          class="absolute -top-2 -right-2 rounded-full bg-green-500 px-2 py-1 text-xs text-white"
        >
          {{ cartItemCount }}
        </span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dropdownOpen: false,
      cartItemCount: 0,
      togleclick() {
        this.cartItemCount++
      },
    }
  },
  methods: {
    toggleDropdown() {
      this.dropdownOpen = !this.dropdownOpen
    },
  },
}
</script>

<style scoped></style>
