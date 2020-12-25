<template>
  <div class="container mx-auto">
    <Navbar />
    <Nuxt />
  </div>
</template>

<script>
import Navbar from "../components/navbar";

export default {
  components: {
    Navbar,
  },
};
</script>