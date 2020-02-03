<template>
    <div class="wrapper">
      <background />
      <Claim />
      <SearchInput v-model="searchValue" @input="handleinput"/>
    </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import background from '@/components/background.vue';

const API = 'https://images-api.nasa.gov/search';


export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    background,
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleinput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:200,400,700&display=swap');


  *{
    box-sizing: border-box;

  }

  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;

  }
  .wrapper{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;
  }

</style>
