<!-- HTML code -->
<template>
  <div class="hero-image" :style="{ backgroundImage }">
    <div
      class="relative smabsolute top-96 md:top-0 md:h-[100%] flex justify-center items-center content-center"
    >
      <h1 class="bg-sky-100 text-center p-6 text-4xl md:text-6xl font-normal m-10">
        Catering for all <span class="cursive--font relative left-1">occasions</span>.
      </h1>
    </div>
    <h2 class="p-3 pl-5 absolute bottom-10 text-white">Lilly's Catering</h2>
    <p class="p-3 pl-5 absolute bottom-5 text-white">90017, Palermo</p>
    <p class="p-3 pl-5 absolute bottom-0 text-white">Sicily, Italy</p>
  </div>
</template>

<!-- JavaScript code -->
<script>
export default {
  data() {
    return {
      backgroundImage: "url('src/assets/catering_bg.jpg')"
    }
  }
}
</script>

<!-- CSS styles -->
<style scoped>
.hero-image {
  width: 100%;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: 0;
}
</style>
