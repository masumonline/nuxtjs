<template>
  <div class="container">
    <div>
      <section class="text-gray-600 body-font">
        <div class="flex flex-col text-center w-full mb-10">
          <h1
            class="text-2xl font-medium title-font mb-4 text-gray-900 tracking-widest"
          >
            BAD JOKE DAD JOKE
          </h1>
          <p class="lg:w-2/3 mx-auto leading-relaxed text-base">
            {{ joke }}
          </p>
        </div>
        <div class="flex flex-col text-center w-full mb-3">
          <h1
            class="text-2xl font-medium title-font mb-4 text-gray-900 tracking-widest"
          >
            Movie List
          </h1>
          <p class="lg:w-2/3 mx-auto leading-relaxed text-base">
            Movie List From themoviedb.org
            <span v-if="!movies.length">Loading...</span>
          </p>
        </div>
        <div class="container px-5 py-10 mx-auto">
          <div class="flex flex-wrap -mx-4 -mb-10 text-center">
            <div
              class="xl:w-1/4 lg:w-1/4 md:w-1/2 sm:w-1/2 mb-10 px-4"
              v-for="movie in movies"
              :key="movie.id"
            >
              <div class="rounded-lg h-auto overflow-hidden">
                <img
                  alt="content"
                  class="object-cover object-center h-auto w-auto loadimg inline"
                  v-bind:src="
                    'https://image.tmdb.org/t/p/w185/' + movie.poster_path
                  "
                />
              </div>
              <h2
                class="title-font text-2xl font-medium text-gray-900 mt-6 mb-3"
              >
                {{ movie.title }}<br />
              </h2>
              <h3 class="title-font text-1xl font-medium text-gray-900">
                Release Date: {{ movie.release_date }}
              </h3>
              <p>Popularity: {{ movie.popularity }}</p>
              <p class="leading-relaxed text-base">
                {{ movie.overview.substring(0, 100) + "..." }}
              </p>
              <button
                class="flex mx-auto mt-6 text-white bg-indigo-500 border-0 py-2 px-5 focus:outline-none hover:bg-indigo-600 rounded"
              >
                Read More
              </button>
            </div>
          </div>
        </div>
      </section>
    </div>
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
  adapter: throttleAdapterEnhancer(axios.defaults.adapter, {
    threshold: 2 * 1000,
  }),
});

const httptwo = axios.create({
  baseURL: "https://api.themoviedb.org/",
  headers: {
    Accept: "application/json",
    "Content-Type": "application/json;charset=utf-8",
    Authorization:
      "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIxZDU5MzY4MGE1YmE1Y2JmNzZjZDQ2NTgyOWRiMmY0YyIsInN1YiI6IjVmZTcwNWNmMTYwZTczMDAzY2FlZDM4YSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.9oSBfZ2J_E58_r7_5BouNO0b2a_ke33ScZADIp8utRM",
  },
  adapter: throttleAdapterEnhancer(axios.defaults.adapter, {
    threshold: 10 * 1000,
  }),
});

export default {
  head() {
    return {
      title: "Nuxt JS Home Page",
    };
  },

  data() {
    return {
      joke: "Loading...",
      movies: [],
    };
  },

  async created() {
    try {
      let res = await http.get("https://icanhazdadjoke.com/");
      this.joke = res.data.joke;
      setTimeout(() => {
        http.get("https://icanhazdadjoke.com/"); // after 2s, the real request makes again
      }, 2 * 1000);
    } catch (error) {
      console.log(error);
    }

    try {
      let res = await httptwo.get(
        "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc"
      );
      this.movies = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
