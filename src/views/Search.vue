<template>
    <div class="wrapper">
      <div class="search">
          <label for="search">Search</label>
          <input id="search"
          name="search"
          v-model="searchValue"
          @input= "handleinput">
          <ul>
            <li v-for="item in results" :key="item.data[0].nasa_id">
              <p>{{ item.data[0].description}}</p>

            </li>
          </ul>
      </div>
    </div>

</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';


export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleinput: debounce(function () {
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
  .wrapper {
    display: flex;
    margin: 0;
    flex-direction: column;
    align-items: center;
    padding: 30px;
    width: 100%;

  }
  .search{
    flex-direction: column;
    width: 200px;
    display: flex;

  }

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid;


  }

</style>
