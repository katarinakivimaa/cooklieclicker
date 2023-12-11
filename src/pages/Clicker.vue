<template>
  <div class="row">
    <div class="col">
      
    </div>
    <div class="col">
      <p class="text-center">Hits {{ cookies }}</p>
      <Gong></Gong>
      
    </div>
    <Upgrades></Upgrades>
  </div>
</template>

<script>
  import Gong from '../components/gong.vue'; import Upgrades from '../components/Upgrades.vue';
          export default {
          components: {
          Gong,
          Upgrades
          }}
</script>
