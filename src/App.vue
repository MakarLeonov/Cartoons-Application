<template>
  <div class="container">
    <p class="title">Cartoons </p>
    <div class="form">
      <my-select :options="dimensions" @changeOption="(value) => currentDimension = value"/>
      <my-select :options="sortingType" @click="(value) => currentSortingType = value"/>
      <my-select :options="genres" @changeOption="(value) => currentGenre = value"/>
      <my-button @click="getCartoons" style="width: 116px;">Sort</my-button>
      <my-input @searchingStr="(value) => searchingStr = value"/>
      <p>Total: {{ totalCartoons }}</p>
    </div>

    <div class="cartoons">
      <v-cartoon v-for="(cartoon, index) in searchedCartoons" :key="index" :cartoon="cartoon"/>
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
import { computed } from 'vue'

export default {
  components: {
    MySelect, MyButton, MyInput, MyPaginationItem, vCartoon
  },

  data() {
    return {
      currentDimension: 'cartoons2D',
      currentGenre: '',
      currentSortingType: '',
      currentPostAmount: '6',
      searchingStr: '',
      totalCartoons: '',

      PostAmount: [
        { value: 6, title: '2D cartoons'},
        { value: 8, title: '3D cartoons'},
        { value: 10, title: '3D cartoons'},
      ],

      dimensions: [
        { value: 'cartoons2D', title: '2D cartoons'},
        { value: 'cartoons3D', title: '3D cartoons'},
      ],

      sortingType: [
        { value: 'cartoons3D', title: 'Without sorting', titleRu: 'Без сортировки'},
        { value: 'cartoons3D', title: 'By releaze date 👆', titleRu: 'По дате релиза 👆'},
        { value: 'cartoons3D', title: 'By releaze date 👇', titleRu: 'По дате релиза 👇'},
        // { value: 'cartoons3D', title: 'Old ones first 🦔', titleRu: 'Сначала старые 🦔'},
        // { value: 'cartoons3D', title: 'New ones first 🐤', titleRu: 'Сначала новые 🐤'},
        { value: 'cartoons3D', title: 'By duration 👇', titleRu: 'По длительности 👆'},
        { value: 'cartoons3D', title: 'By duration 👆', titleRu: 'По длительности 👇'},
        { value: 'cartoons3D', title: 'By epizodes amount 👇', titleRu: 'По кол-ву эпизодов 👆'},
        { value: 'cartoons3D', title: 'By epizodes amount 👆', titleRu: 'По кол-ву эпизодов 👇'},
      ],

      genres: [{value: '', title: 'All genres'}],
      genresArr: [],
      cartoons: [],
    }
  },

  methods: {

    async getCartoons() {
      let response = await fetch(`https://api.sampleapis.com/cartoons/${this.currentDimension}`)
      this.cartoons = await response.json()
      // console.log(this.currentDimension, this.currentGenre, this.currentSortingType)

    },

    getGenres(cartoons) {
      cartoons.forEach(cartoon => {
        cartoon.genre.forEach(item => {
          (this.genresArr.includes(item)) ? false : (this.genresArr.push(item) && this.genres.push({value: item, title: item}));
        })
      })
    }

  },

  async mounted() {
    await this.getCartoons(this.currentDimension)
    this.getGenres(this.cartoons)
    console.log(this.cartoons)
  },

  computed: {
    sortedCartoons() {
      return this.cartoons.filter(cartoon => {
        return (cartoon.genre.includes(this.currentGenre) || this.currentGenre === '') ? true : false;
      })
    },

    searchedCartoons() {
      return this.cartoons.filter(cartoon => {
        return cartoon.creator[0].toUpperCase().includes(this.searchingStr.toUpperCase()) 
                || cartoon.title.toUpperCase().includes(this.searchingStr.toUpperCase())
                || this.searchingStr === ''
      })
    }
  },

  watch: {  
    cartoons(){
      this.totalCartoons = this.cartoons.length
    }
  },

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
