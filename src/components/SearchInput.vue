<template>
  <div class="searchWrapper">
    <input id="search"
    name="search"
    v-model="searchValue"
    @input= "handleinput">

  </div>
</template>

<script>
export default {
  name: 'SearchInput',
};
</script>

<style lang="scss" scoped>

  .searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;


  input {
    background: none;
    height: 30px;
    border: 0;
    border-bottom: 1px solid;

    }
  }
</style>
