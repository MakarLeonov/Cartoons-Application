<template>
  <div class="container">
    <p class="title">Cartoons </p>
    <div class="form">
      <my-select :options="dimensions" @changeOption="(value) => currentDimension = value"/>
      <!-- <my-select />
      <my-select :genres="genres"/> -->
      <my-button @click="getCartoons" style="width: 124px;">Sort</my-button>
      <my-input />
    </div>

    <div class="cartoons">
      <v-cartoon v-for="(cartoon, index) in cartoons" :key="index" :cartoon="cartoon"/>
    </div>

    <div class="bottom">
      <div class="pagination">
        <my-pagination-item>1</my-pagination-item>
        <my-pagination-item>2</my-pagination-item>
        <my-pagination-item>3</my-pagination-item>
        <my-pagination-item>4</my-pagination-item>
      </div>
      <!-- <my-select /> -->
    </div> 
  </div>
</template>

<script>
import MySelect from "@/components/UI/MySelect.vue" 
import MyButton from "@/components/UI/MyButton.vue" 
import MyInput from "@/components/UI/MyInput.vue" 
import MyPaginationItem from "@/components/UI/MyPaginationItem.vue" 
import vCartoon from "@/components/vCartoon.vue" 

export default {
  components: {
    MySelect, MyButton, MyInput, MyPaginationItem, vCartoon
  },

  data() {
    return {
      currentDimension: 'cartoons2D',
      currentGenre: '',
      sortingType: '',

      dimensions: [
        { value: 'cartoons2D', title: '2D cartoons'},
        { value: 'cartoons3D', title: '3D cartoons'},
      ],
      genres: [{vaule: '', title: 'All genres'},],
      cartoons: [],
    }
  },

  methods: {

    async getCartoons() {
      let response = await fetch(`https://api.sampleapis.com/cartoons/${this.currentDimension}`)
      this.cartoons = await response.json()
    },

    getGenres(cartoons) {
      cartoons.forEach(cartoon => {
        cartoon.genre.forEach(item => {
          this.genres.forEach(obj => {
            (obj.title === item) ? false : console.log(true)
          })
        })
      })

      console.log(this.genres)
    }

    
  },



  async mounted() {
    await this.getCartoons(this.currentDimension)
    this.getGenres(this.cartoons)
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
