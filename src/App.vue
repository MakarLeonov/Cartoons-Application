<template>
  <div class="container">
    <p class="title">Cartoons </p>
    <div class="form">
      <my-header />
      <my-header />
      <my-header />
      <my-button style="width: 124px;">Sort</my-button>
      <my-input />
    </div>

    <div class="cartoons">
      <div class="cartoon">
        <img src="https://nick.mtvnimages.com/uri/mgid:arc:content:nick.com:9cd2df6e-63c7-43da-8bde-8d77af9169c7?quality=0.7" alt="image">
        <div class="cartoon-info">
            <p class="name">Spongebob Squarepants</p>
            <p class="author">by Stephen Hillenburg</p>
            <p class="paragraph">Year: 1990</p>
            <p class="paragraph">Epizodes: 279</p>
            <p class="paragraph">Runtime: 22 min</p>
            <p class="paragraph">Genre: Comedy, Family</p>
        </div>
      </div>
      <div class="cartoon">
        <img src="https://nick.mtvnimages.com/uri/mgid:arc:content:nick.com:9cd2df6e-63c7-43da-8bde-8d77af9169c7?quality=0.7" alt="image">
        <div class="cartoon-info">
            <p class="name">Spongebob Squarepants</p>
            <p class="author">by Stephen Hillenburg</p>
            <p class="paragraph">Year: 1990</p>
            <p class="paragraph">Epizodes: 279</p>
            <p class="paragraph">Runtime: 22 min</p>
            <p class="paragraph">Genre: Comedy, Family</p>
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
      <my-header />
    </div>
  </div>
</template>

<script>
import MyHeader from "@/components/UI/MyHeader.vue" 
import MyButton from "@/components/UI/MyButton.vue" 
import MyInput from "@/components/UI/MyInput.vue" 
import MyPaginationItem from "@/components/UI/MyPaginationItem.vue" 

export default {
  components: {
    MyHeader, MyButton, MyInput, MyPaginationItem
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
