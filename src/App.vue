<template>
  <div class="bg-white w-screen h-screen flex items-center justify-center kk">
    <ContainerDragBox/>
  </div>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';
import ContainerDragBox from './components/container.vue';

export default defineComponent({
  name: 'App',
  components: {
    ContainerDragBox,
  },
});
  
</script>

<style lang='postcss' scoped>

</style>