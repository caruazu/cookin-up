<script lang="ts">
  import Banner from './components/Banner.vue';
  import ComponentePrincipal from './components/ComponentePrincipal.vue';
import Rodape from './components/Rodape.vue';

  export default {
    components: {Banner,ComponentePrincipal, Rodape}
  }
</script>

<template>
  <Banner/>
  <ComponentePrincipal/>
  <Rodape/>
</template>

<style scoped>

</style>