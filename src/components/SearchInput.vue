<template>
    <input id="search"
    name="search"
    :value="value"
    @input="handlechange">
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    handlechange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>

  input {
    background: none;
    text-align: center;
    font-size: 18px;
    height: 30px;
    border: 0;
    border-bottom: 1px solid;
    color: white;
    transition: box-shadow .4s;
    font-family: 'Montserrat';

  }

    input:focus {
      outline: none;
      box-shadow: 0 8px 15px -8px white;
    }

</style>
