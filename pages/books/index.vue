<template>
  <div>
    <section class="text-gray-700 body-font">
      <div class="container px-5 py-24 mx-auto">
        <div class="flex flex-wrap -m-4">
          <div class="p-4 md:w-1/3" v-for="book in books" :key="book.id">
            <div
              class="h-full border-2 border-gray-200 rounded-lg overflow-hidden"
            >
              <img
                class="lg:h-48 md:h-36 w-full object-cover object-center"
                v-bind:src="book.photo"
                alt="Book"
              />
              <div class="p-6">
                <h2
                  class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1"
                >
                  Book
                </h2>
                <h1 class="title-font text-lg font-medium text-gray-900 mb-3">
                  {{ book.name }}
                </h1>
                <p class="leading-relaxed mb-3">
                  {{ book.description }}
                </p>
                <p>Price: {{ book.price }}</p>
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
export default {
  head() {
    return {
      title: "Book From Api",
    };
  },

  data() {
    return {
      books: [],
    };
  },

  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };

    try {
      const res = await axios.get("https://api.bddevwork.net/book", config);
      this.books = res.data.data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>