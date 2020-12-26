<template>
  <div>
    <section class="text-gray-700 body-font">
      <h1
        class="text-center text-2xl font-medium title-font mb-4 text-gray-900 tracking-widest"
        v-if="!users.length"
      >
        Loading ...
      </h1>
      <div class="container px-5 py-24 mx-auto">
        <div class="flex flex-wrap -m-4">
          <div class="p-4 md:w-1/4" v-for="user in users" :key="user.id">
            <div
              class="h-full border-2 border-gray-200 rounded-lg overflow-hidden"
            >
              <img
                class="lg:h-48 md:h-36 w-full object-cover object-center loadimg"
                v-bind:src="user.photo"
                alt="User"
              />
              <div class="p-6">
                <h2
                  class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1"
                >
                  User
                </h2>
                <h1 class="title-font text-lg font-medium text-gray-900 mb-3">
                  {{ user.name }}
                </h1>
                <p class="leading-relaxed mb-3">
                  {{ user.email }}
                </p>
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
  baseURL: "https://api.bddevwork.net/user",
  headers: { Accept: "application/json" },
  adapter: throttleAdapterEnhancer(
    cacheAdapterEnhancer(axios.defaults.adapter)
  ),
});

export default {
  head() {
    return {
      title: "User From Api",
    };
  },

  data() {
    return {
      users: [],
    };
  },

  async created() {
    try {
      const res = await http.get("https://api.bddevwork.net/user");
      this.users = res.data.data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>