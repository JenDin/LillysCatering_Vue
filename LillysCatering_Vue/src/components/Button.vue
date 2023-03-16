<!-- HTML code -->
<template>
  <button
    class="p-2 uppercase font-semibold bg-black text-white w-full hover:bg-[#457b9d] hover:text-white"
  >
    {{ btnText }}
  </button>
</template>

<!-- JavaScript code -->
<script>
import { RouterLink } from 'vue-router'
export default {
  name: 'Button',
  props: {
    btnText: String
  }
}
</script>

<!-- CSS styles -->
<style scoped></style>
