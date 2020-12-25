<template>
  <div>
    <header class="text-gray-700 body-font">
      <div
        class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center"
      >
        <nuxt-link
          to="/"
          class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            class="w-10 h-10 text-white p-2 bg-indigo-500 rounded-full"
            viewBox="0 0 24 24"
          >
            <path
              d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"
            ></path>
          </svg>
          <span class="ml-3 text-xl">NUXT JS</span>
        </nuxt-link>
        <nav
          class="md:ml-auto flex flex-wrap items-center text-base justify-center"
        >
          <nuxt-link to="/" class="mr-5 hover:text-gray-900"> Home </nuxt-link>
          <nuxt-link to="/about" class="mr-5 hover:text-gray-900">
            About
          </nuxt-link>
          <nuxt-link to="/books" class="mr-5 hover:text-gray-900">
            Books
          </nuxt-link>
          <nuxt-link to="/users" class="mr-5 hover:text-gray-900">
            Users
          </nuxt-link>
          <nuxt-link to="/bad" class="mr-5 hover:text-gray-900">
            Braking Bad
          </nuxt-link>
        </nav>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: "Navbar",
};
</script>

<style>
</style>