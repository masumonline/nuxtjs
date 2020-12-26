
<template>
  <div>
    <section class="text-gray-700 body-font">
      <div class="container px-5 py-24 mx-auto">
        <div class="flex flex-wrap -m-4">
          <div class="p-4 md:w-1/3" v-for="bad in bads" :key="bad.id">
            <div
              class="h-full border-2 border-gray-200 rounded-lg overflow-hidden"
            >
              <img
                class="lg:h-48 md:h-36 w-full object-cover object-center loadimg"
                v-bind:src="bad.img"
                alt="Bad"
              />
              <div class="p-6">
                <h2
                  class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1"
                >
                  {{ bad.nickname }}
                </h2>
                <h1 class="title-font text-lg font-medium text-gray-900 mb-3">
                  {{ bad.name }}
                </h1>
                <p class="leading-relaxed mb-3">
                  {{ bad.status }}
                </p>
                <p>Birthday: {{ bad.birthday }}</p>
              </div>
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
  baseURL: "https://breakingbadapi.com/api/characters",
  headers: { Accept: "application/json" },
  adapter: throttleAdapterEnhancer(
    cacheAdapterEnhancer(axios.defaults.adapter)
  ),
});

export default {
  head() {
    return {
      title: "Braking Bad API",
    };
  },

  data() {
    return {
      bads: [],
    };
  },

  async created() {
    try {
      const res = await http.get("https://breakingbadapi.com/api/characters");
      this.bads = res.data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>