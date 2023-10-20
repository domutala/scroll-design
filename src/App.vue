<script setup lang="ts">
import ScrollDesign from '@/components/ScrollDesign.vue'
import ScrollDesignContainer from '@/components/ScrollDesignContainer.vue'
</script>

<template>
  <scroll-design-container>
    <scroll-design
      v-for="i in 10"
      :key="i"
      :line-color="
        i % 2 === 0
          ? 'linear-gradient(0deg, rgba(255,255,255,1) 0%, rgba(9,9,121,1) 100%)'
          : 'linear-gradient(0deg, rgba(9,9,121,1) 0%, rgba(255,255,255,1) 100%)'
      "
    ></scroll-design>
  </scroll-design-container>
</template>
