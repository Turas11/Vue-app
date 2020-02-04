<template>
  <div :class="[{ flexstart: step === 1}, 'wrapper']">
      <transition name="slide">
      <p class="logo" v-if="step === 1">SPACER</p>
       </transition>
      <transition name="component-fade">
        <background v-if="step === 0" />
      </transition>
      <Claim v-if="step === 0"/>
      <SearchInput v-model="searchValue" @input="handleinput" :dark="step === 1"/>
      <div class="results" v-if="results && !loading && step === 1">
          <item v-for="item in results" :item="item" :key="item.data[0].nasa_id"
          @click.native="handleModalOpen(item)" />
      </div>
      <div class="loader" v-if="step === 1 && loading" />
      <modal v-if="modalOpen" @closeModal="modalOpen = false" :item="modalItem" />
    </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import background from '@/components/background.vue';
import item from '@/components/item.vue';
import modal from '@/components/modal.vue';

const API = 'https://images-api.nasa.gov/search';


export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    background,
    item,
    modal,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
      modalOpen: false,
      modalItem: [],
    };
  },
  methods: {
    handleModalOpen(it) {
      this.modalOpen = true;
      this.modalItem = it;
    },
    handleinput: debounce(function () {
      this.loading = true;

      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
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

  .component-fade-enter-active, .component-fade-leave-active {
    transition: opacity .7s ease;
  }
  .component-fade-enter, .component-fade-leave-to
  {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, .slide-leave-to
  {
    margin-top: -50px;
  }

  .wrapper{
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;

    &.flexstart {
    justify-content: flex-start;

    }
  }
  .logo {
    position: absolute;
    top: 20px;
    font-size: 20px;
    letter-spacing: 2px;
    font-weight: 600;


  }
  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px;

    @media (max-width: 768px) {
    grid-template-columns: 1fr 1fr;
    }

    @media (max-width: 950px) {
    grid-template-columns: 1fr 1fr;
    }


    @media (max-width: 480px) {
    grid-template-columns: 1fr;
    }

  }

.loader {
  margin-top: 100px;
  display: inline-block;
  width: 80px;
  height: 80px;
}
.loader:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #4C1F96;
  border-color: #4C1F96 transparent #4C1F96 transparent;
  animation: loading 1.2s linear infinite;
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}


</style>
