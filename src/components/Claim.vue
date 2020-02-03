<template>
<div class="claimwrapper">
  <h1 class="claim">SPACER</h1>
  <p class = "subclaim">Begin your journey through our amazing galaxy,
  and discover places you never even heard.</p>
  <p class="subclaim">Type antyching space-related to start</p>
</div>
</template>

<script>
export default {
  name: 'Claim',

};
</script>

<style lang="scss" scoped>
  .claimwrapper {
    display: flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .claim {
    font-size: 50px;
    margin: 0;

  }

  .subclaim {
    margin-top: 20px 0 0 0;
    font-size: 13px;

  }
</style>
