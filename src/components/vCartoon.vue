<template>
    <div class="cartoon">
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
</template>
<script>
export default {
    name: 'vCartoon',
    props: {
        cartoon: {
            type: Object,
        }
    }
    
}
</script>
<style lang="scss" scoped>

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
    
</style>