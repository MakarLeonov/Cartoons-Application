<template>
  <div class="container">
    <p class="title">Cartoons </p>
    <div class="form">
      <my-select :options="dimensions" @changeOption="(value) => currentDimension = value"/>
      <my-select :options="sortingType" @changeOption="(value) => asd(value)"/>
      <my-select :options="genres" @changeOption="(value) => currentGenre = value"/>
      <my-button @click="getCartoons" style="width: 116px;">Sort</my-button>
      <my-input @searchingStr="(value) => searchingStr = value"/>
      <p class="total">Total: {{ totalCartoons }}</p>
    </div>

    <div class="cartoons">
      <v-cartoon 
        v-for="(cartoon, index) in paginatedCartoons" 
        :key="index" 
        :cartoon="cartoon"
        
        />
    </div>

    <div class="bottom">
      <div class="pagination" >
        <my-pagination-item 
          v-for="(page, index) in currentPostAmount" 
          :key="page"
          :page="page"
          @click="pageNumber = page"
          :pageNumber="pageNumber"
          >
          {{ index + 1 }}
        </my-pagination-item>
      </div>
      <!-- <my-select :options="PostAmount" @changeOption="(value) => currentPostAmount = value"/> -->
        
        <a href="https://github.com/MakarLeonov/Cartoons-Application" target="_blank">
          <my-button>Repo</my-button>
        </a>
    </div> 

    <footer>
      <p>© 2023, dev by Leonov Makar</p>
    </footer>
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
      currentSortingDir: false,
      currentPostAmount: null,
      searchingStr: '',
      totalCartoons: '',

      cartoonsPerPage: 6,
      pageNumber: 1,

      // PostAmount: [
      //   { value: 4, title: '4 cartoons'},
      //   { value: 6, title: '6 cartoons'},
      // ],

      dimensions: [
        { value: 'cartoons2D', title: '2D cartoons'},
        { value: 'cartoons3D', title: '3D cartoons'},
      ],

      sortingType: [
        { value: '', title: 'Without sorting', titleRu: 'Без сортировки'},
        { value: ['year', true], title: 'By releaze date 👆', titleRu: 'По дате релиза 👆'},
        { value: ['year', false], title: 'By releaze date 👇', titleRu: 'По дате релиза 👇'},
        // { value: 'cartoons3D', dir: true, title: 'Old ones first 🦔', titleRu: 'Сначала старые 🦔'},
        // { value: 'cartoons3D', dir: true, title: 'New ones first 🐤', titleRu: 'Сначала новые 🐤'},
        { value: ['runtime_in_minutes', false], title: 'By duration 👇', titleRu: 'По длительности 👆'},
        { value: ['runtime_in_minutes', true], title: 'By duration 👆', titleRu: 'По длительности 👇'},
        { value: ['episodes', false], title: 'By epizodes amount 👇', titleRu: 'По кол-ву эпизодов 👆'},
        { value: ['episodes', true], title: 'By epizodes amount 👆', titleRu: 'По кол-ву эпизодов 👇'},
      ],

      genres: [{value: '', title: 'All genres'}],
      genresArr: [],
      cartoons: [],
    }
  },

  methods: {

    async getCartoons() {
      let response = await fetch(`https://api.sampleapis.com/cartoons/${this.currentDimension}`)
      let cartoons = await response.json()
      await this.getGenres(cartoons)
      this.cartoons = await cartoons.filter(cartoon => (cartoon.genre.includes(this.currentGenre) || this.currentGenre === '') ? true : false)
      this.sorteBySetParam(this.currentSortingType, this.currentSortingDir)


      if (this.currentSortingType != ''){
        console.log('Type: ', this.currentSortingType, 'Dir: ', this.currentSortingDir)
      }
      this.pageNumber = 1;

    },

    async getGenres(cartoons) {
      await this.genresArr.splice(0)
      await this.genres.splice(1)
      cartoons.forEach(cartoon => {
        cartoon.genre.forEach(item => {
          (this.genresArr.includes(item)) ? false : (this.genresArr.push(item) && this.genres.push({value: item, title: item}));
        })
      })
    },

    sorteBySetParam(prop, dir = false) {
      if (this.currentSortingType != '') {
        this.cartoons.sort((a, b) => (!dir ? a[prop] < b[prop] : a[prop] > b[prop]) ? -1 : 1)
      }
    },

    asd(value) {
      this.currentSortingType = value[0] 
      this.currentSortingDir = value[1]
    }

  },

  async mounted() {
    await this.getCartoons(this.currentDimension)
    this.getGenres(this.cartoons)

    this.currentPostAmount = Math.ceil(this.cartoons.length/6);
  },

  computed: {
    // sortedCartoons() {
    //   return this.cartoons.filter(cartoon => {
    //     return (cartoon.genre.includes(this.currentGenre) || this.currentGenre === '') ? true : false;
    //   })
    // },

    searchedCartoons() {
      return this.cartoons.filter(cartoon => {
        return cartoon.creator[0].toUpperCase().includes(this.searchingStr.toUpperCase()) 
                || cartoon.title.toUpperCase().includes(this.searchingStr.toUpperCase())
                || this.searchingStr === ''
      })
    },

    paginatedCartoons() {
      let from = (this.pageNumber - 1) * this.cartoonsPerPage;
      let to = from + this.cartoonsPerPage

      return this.searchedCartoons.slice(from, to)
    }
  },

  watch: {  
    cartoons(){
      this.totalCartoons = this.cartoons.length
      this.currentPostAmount = Math.ceil(this.cartoons.length/this.cartoonsPerPage);
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

  position: relative;
	min-height: 100%;
}

.title {
  width: fit-content;
  font-weight: 700;
  font-size: 128px;
  line-height: 143px;
  margin: 140px 0 30px;

  background: linear-gradient(91.93deg, #F0474A 6.29%, #EDF5E1 27.77%, #FDAF1A 47.56%, #0B91CD 66.51%, #0E3A5D 78.72%, #0E3A5D 87.15%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
}

.cartoons {
  min-height: 450px;
}

.form, .cartoons {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
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

.total {
  font-size: 25px;
  color: #EDF5E1;
}


.bottom {
  display: flex;
  justify-content: space-between;
  margin-bottom: 70px;

  .pagination {
    display: flex;
    gap: 10px;
  }
}

a {
  text-decoration: none;
}

footer {
  width: 100%;

  & > p {
    color: #EDF5E1;
    font-size: 15px;
    text-align: center;
    margin-bottom: 10px;
  }
}



</style>
