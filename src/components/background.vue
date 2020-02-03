<template lang="html">
  <div class="backwrapper">

  </div>

</template>

<script>
export default {
  name: 'background',
};
</script>

<style lang="scss" scoped>
.backwrapper{
  position: fixed;
  width: 100%;
  height: 100vh;
  z-index: -1;
  top: 0;
  background-image: url('../assets/background.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 0%;
}

</style>
