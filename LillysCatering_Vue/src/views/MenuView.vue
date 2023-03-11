<!-- HTML code -->
<template>
  <h1 class="text-4xl text-center uppercase font-bold mt-8 mb-10">Catering menus</h1>

  <div>
    <MediterraneanMenu v-for="dish in dishes" :dish="dish" :key="dish.id" />
  </div>
  <Footer />
</template>

<!-- JavaScript code -->
<script>
import MediterraneanMenu from '../components/MediterraneanMenu.vue'
import Footer from '../components/Footer.vue'
export default {
  components: {
    Footer,
    MediterraneanMenu
  },
  data() {
    return {
      dishes: []
    }
  },
  methods: {
    async getDishes() {
      const resp = await fetch('https://localhost:7235/api/dish')
    }
  }
}
</script>

<!-- CSS styles -->
<style scoped></style>
