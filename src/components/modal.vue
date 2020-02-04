<template>
  <div class="outerwrapper">
    <div class="innerwrapper">
      <div class="photo">
        <img :src="photo">
      </div>
      <div class="description">
        <h2>{{ title }}</h2>
        <p class="description">
          {{description}}
        </p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')" />
  </div>
</template>

<script>
export default {
  name: 'modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 400);
  },
};
</script>

<style lang="scss" scoped>
  .outerwrapper{
    background: #f6f6f6;
    height: 100%;
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;

    @media(min-width: 1024px){
      max-width: 70%;
      height: 50%;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      box-shadow: 20px 20px 20px -9px #4F4850;
    }
  }

  .close {
    position: absolute;
    width: 30px;
    height: 30px;
    right: 0;
    top: 0;
    padding: 30px;
    cursor: pointer;

    &::before,
    &::after {
      position: absolute;
      content: '';
      width: 10px;
      top: 30px;
      right: 20px;
      height: 2px;
      background: black;
      display: block;
    }
    &::before {
      transform: rotate(45deg);

    }

    &::after {
      transform: rotate(-45deg);

    }

  }

  .innerwrapper{
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-direction: column;

  @media(min-width: 1024px){
    flex-direction: row;
    .photo {
      min-width: 50%;
      margin-right: 30px;
    }
  }

}

  .photo {
    width: auto;
    height: auto;
    background: block;

    img {
      width: 70%;
      height: 70%;
    }
  }

</style>
