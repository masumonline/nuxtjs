
<template>
  <div>
    <section class="text-gray-600 body-font">
      <h1
        class="text-center text-2xl font-medium title-font mb-4 text-gray-900 tracking-widest"
        v-if="!jokes"
      >
        Loading ...
      </h1>
      <div class="container px-5 py-24 mx-auto flex flex-wrap">
        <div
          class="flex relative pt-10 pb-20 sm:items-center md:w-2/3 mx-auto"
          v-for="(joke, index) in jokes"
          :key="joke.id"
        >
          <div
            class="h-full w-6 absolute inset-0 flex items-center justify-center"
          >
            <div class="h-full w-1 bg-gray-200 pointer-events-none"></div>
          </div>
          <div
            class="flex-shrink-0 w-6 h-6 rounded-full mt-10 sm:mt-0 inline-flex items-center justify-center bg-indigo-500 text-white relative z-10 title-font font-medium text-sm"
          >
            {{ index + 1 }}
          </div>
          <div
            class="flex-grow md:pl-8 pl-6 flex sm:items-center items-start flex-col sm:flex-row"
          >
            <div
              class="flex-shrink-0 w-24 h-24 bg-indigo-100 text-indigo-500 rounded-full inline-flex items-center justify-center"
            >
              <svg
                fill="none"
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                class="w-12 h-12"
                viewBox="0 0 24 24"
              >
                <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"></path>
              </svg>
            </div>
            <div class="flex-grow sm:pl-6 mt-6 sm:mt-0">
              <h2 class="font-medium title-font text-gray-900 mb-1 text-xl">
                {{ joke.id }}
              </h2>
              <p class="leading-relaxed">
                {{ joke.joke }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import {
  cacheAdapterEnhancer,
  throttleAdapterEnhancer,
} from "axios-extensions";

const http = axios.create({
  baseURL: "https://icanhazdadjoke.com/",
  headers: { Accept: "application/json" },
  adapter: throttleAdapterEnhancer(
    cacheAdapterEnhancer(axios.defaults.adapter)
  ),
});

export default {
  head() {
    return {
      title: "Bad Dad Joke",
    };
  },

  data() {
    return {
      jokes: [],
    };
  },

  async created() {
    try {
      const res = await http.get("https://icanhazdadjoke.com/search");
      this.jokes = res.data.results;
      console.log(res.data);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>