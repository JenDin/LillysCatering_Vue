<!-- HTML code -->
<template>
  <p v-if="dish.menuId === 3">{{ dish.title }}</p>
  <p v-if="dish.menuId === 3" class="text-sm italic mb-3">{{ dish.ingredients }}</p>
</template>

<!-- JavaScript code -->
<script>
export default {
  props: {
    dish: Object
  }
}
</script>

<!-- CSS styles -->
<style scoped></style>
