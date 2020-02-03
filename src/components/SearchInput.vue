<template>
    <input id="search"
    name="search"
    :value="value"
    @input="handlechange"
    :class="{ dark }">

</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,

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

    .dark {
      color: #4C1F96;
      border-bottom-color: #4C1F96;
      margin-top: 50px;
    }

    .dark:focus {
      color: #4C1F96;
      box-shadow: 0 8px 15px -8px #4C1F96;
    }

</style>
