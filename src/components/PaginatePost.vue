<script setup lang="ts">
import {computed} from "vue";

defineProps({
  start:Number,
  end:Number,
  maximum:Number
})
const emit = defineEmits(['next', 'prev'])


</script>

<template>
 <div class="btn-group" role="group" aria-label="Basic example">
   <button
       class="btn btn-outline-primary"
       @click="emit('prev')"
       type="button"
       :disabled="(start===0)"
   >Previous</button>
   <button
       class="btn btn-outline-primary"
       @click="emit('next')"
       type="button"
       :disabled="end >= maximum"
   >Next</button>
 </div>
</template>

<style scoped>

</style>