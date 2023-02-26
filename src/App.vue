<template>
  <div class="container">
    <p class="title">Cartoons </p>
    <div class="form">
      <my-select />
      <my-select />
      <my-select />
      <my-button style="width: 124px;">Sort</my-button>
      <my-input />
    </div>

    <div class="cartoons">
      <div class="cartoon" v-for="(cartoon, index) in cartoons" :key="index">
        <img :src="cartoon.image" alt="image not found😢">
        <div class="cartoon-info">
            <p class="name">{{ cartoon.title }}</p>
            <p class="author">by {{ cartoon.creator[0] }}</p>
            <p class="paragraph">Year: {{ cartoon.year }}</p>
            <p class="paragraph">Epizodes: {{ cartoon.episodes }}</p>
            <p class="paragraph">Runtime: {{ cartoon.runtime_in_minutes }} min</p>
            <p class="paragraph">Genre: {{ cartoon.genre.join(', ') }}</p>
        </div>
      </div>
    </div>

    <div class="bottom">
      <div class="pagination">
        <my-pagination-item>1</my-pagination-item>
        <my-pagination-item>2</my-pagination-item>
        <my-pagination-item>3</my-pagination-item>
        <my-pagination-item>4</my-pagination-item>
      </div>
      <my-select />
    </div> 
  </div>
</template>

<script>
import MySelect from "@/components/UI/MySelect.vue" 
import MyButton from "@/components/UI/MyButton.vue" 
import MyInput from "@/components/UI/MyInput.vue" 
import MyPaginationItem from "@/components/UI/MyPaginationItem.vue" 

export default {
  components: {
    MySelect, MyButton, MyInput, MyPaginationItem
  },

  data() {
    return {
      currentDimension: 'cartoons2D',
      dimensions: ['cartoons2D', 'cartoons3D'],
      cartoons: [],
    }
  },

  methods: {
    async getCartoons(dimension) {
      let response = await fetch(`https://api.sampleapis.com/cartoons/${this.currentDimension}`)
      this.cartoons = await response.json()
      console.log(this.cartoons)
    }
  },



  async mounted() {
    this.getCartoons(this.currentDimension)
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Comfortaa', cursive;
}

body {
  background: #1E1E1E;
}

.container {
  width: 1520px;
  margin: 0 auto;
}

.title {
  width: fit-content;
  font-weight: 700;
  font-size: 128px;
  line-height: 143px;
  margin: 140px 0 40px;

  background: linear-gradient(91.93deg, #F0474A 6.29%, #EDF5E1 27.77%, #FDAF1A 47.56%, #0B91CD 66.51%, #0E3A5D 78.72%, #0E3A5D 87.15%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
}

.form, .cartoons {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;

  -webkit-touch-callout: none;
    -webkit-user-select: none;
     -khtml-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
            user-select: none;
}

.form {
  margin-bottom: 30px;
}

.cartoon {
  width: 750px;
  height: 450px;
  color: #EDF5E1;

  display: flex;
  gap: 20px;
  margin-bottom: 30px;
  transition: all .2s ease-out;

  &:hover {
    background: hsla(0, 0%, 100%, 0.018);
    box-shadow: 0px 0px 15px rgba($color: #000000, $alpha: 0.16);
    transition: all .2s ease-in;
  }
  
  img {
    height: 100%;
    width: 300px;
  }

  .name {
    margin-top: 190px;
    font-weight: 700;
    font-size: 27px;
    line-height: 30px;
  }

  .paragraph, .author {
    margin-top: 7px;
    font-weight: 400;
    font-size: 20px;
    line-height: 22px;
  }

  .author {
    margin-bottom: 37px;
  }
}


.bottom {
  display: flex;
  justify-content: space-between;
  margin-bottom: 50px;

  .pagination {
    display: flex;
    gap: 10px;
  }
}



</style>
