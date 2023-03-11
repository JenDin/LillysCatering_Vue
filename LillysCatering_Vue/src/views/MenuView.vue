<!-- HTML code -->
<template>
  <h1 class="text-4xl text-center uppercase font-bold mt-8 mb-6">Catering menus</h1>
  <p class="text-center p-2 pt-0 lg:w-1/2 mx-auto mb-12 leading-7">
    Our menus offer a top-notch restaurant-caliber culinary experience, featuring the highest
    quality as local, seasonal, organic and sustainably farmed ingredients as possible. Whether
    you're planning a wedding reception, corporate event, or private party, our food catering menus
    will surely impress your guests and exceed your expectations.
  </p>

  <div class="m-6">
    <div
      class="border-2 border-black mx-auto md:flex p-4 justify-center gap-6 xl:gap-2 max-w-5xl mb-40"
    >
      <div class="xl:w-1/2 mb-8 lg:mb-0">
        <h2 class="text-3xl font-bold mb-2">Mediterranean</h2>
        <MediterraneanMenu v-for="dish in dishes" :dish="dish" :key="dish" />
        <div class="bg-[#e5d9f2] p-2 w-72">
          <p class="mb-1">
            <span class="font-bold">Minium guest amount:</span> {{ mediterreanAmount }} people
          </p>
          <p><span class="font-bold">Price:</span> ${{ mediterraneanPrice }}/person</p>
        </div>
      </div>
      <div class="xl:w-1/2">
        <h2 class="text-3xl font-bold mb-2">Italian</h2>
        <ItalianMenu v-for="dish in dishes" :dish="dish" :key="dish" />
        <div class="bg-[#e5d9f2] p-2 w-72">
          <p class="mb-1">
            <span class="font-bold">Minium guest amount:</span> {{ italianAmount }} people
          </p>
          <p><span class="font-bold">Price:</span> ${{ italianPrice }}/person</p>
        </div>
      </div>
    </div>
  </div>

  <Footer />
</template>

<!-- JavaScript code -->
<script>
import MediterraneanMenu from '../components/MediterraneanMenu.vue'
import ItalianMenu from '../components/ItalianMenu.vue'
import Footer from '../components/Footer.vue'
export default {
  components: {
    Footer,
    MediterraneanMenu,
    ItalianMenu
  },
  data() {
    return {
      dishes: [],
      mediterraneanPrice: '',
      italianPrice: '',
      mediterreanAmount: '',
      italianAmount: ''
    }
  },
  methods: {
    async getDishes() {
      const resp = await fetch('https://localhost:7235/api/dishapi')

      const data = await resp.json()

      this.dishes = data

      // Prices
      this.mediterraneanPrice = data[0].menu.price
      this.italianPrice = data[7].menu.price

      // Guest amount
      this.mediterreanAmount = data[0].menu.minGuestAmount
      this.italianAmount = data[7].menu.minGuestAmount
    }
  },
  mounted() {
    this.getDishes()
  }
}
</script>

<!-- CSS styles -->
<style scoped></style>
