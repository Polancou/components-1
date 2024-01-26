<script setup lang="ts">
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  id: {
    type: Number,
    required: true,
  },
  body: {
    type: String,
    required: false,
    default: 'No description',
  }
})

const emit = defineEmits(['changeFavorite'])



</script>

<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{id}} {{title}}</h5>
      <p class="card-text">{{ body }}</p>
      <button
          class="btn btn-outline-primary"
          @click="$emit('changeFavorite',title)"
      >Favorite</button>
    </div>
  </div>
</template>

<style scoped>

</style>