<template>
  <div class="gallery-wrapper">
      <div class="gallery-wrapper__card" v-for="item in books" :key="item['id']">
          <img :src="item.volumeInfo.imageLinks.thumbnail" class="gallery-wrapper__card__thumb" alt="">
          <h2>{{ item.volumeInfo.title }}</h2>
          <h3>{{ item.volumeInfo.authors[0] }}</h3>
          <CardButtons />
      </div>
  </div>
</template>

<script>
import axios from 'axios'
import CardButtons from './CardButtons.vue'

export default {
    components: {
        CardButtons
    },
  data () {
    return {
      books: [],
      loading: true,
      cart: 0,
    }
  },
  mounted () {
    axios
      .get('https://www.googleapis.com/books/v1/volumes?q=food')
      .then(response => (this.books = response.data.items))

  }
}

</script>

<style lang="scss">

$font-size-h2: 15px;
$font-size-h3: 0.82*$font-size-h2;
$width: 30%;

.gallery-wrapper{
    display:flex;
    width:100%;
    flex-wrap: wrap;
    flex-direction: row;
    justify-content: center;

    &__card {
        width: $width;
        background-color:#f1eeee;
        margin:10px;
        padding:15px 0px 15px 0px;

        &:hover {
        background-color:#e6e6e6;
        }

        &__thumb{
            height:200px;
        }

        h2 {
            color:black;
            font-size: $font-size-h2;
            margin-bottom: 0.3*($font-size-h2);
        }

        h3 {
            color:#909090;
            font-size: $font-size-h3;
            margin-top: 0px;
        }
    }
}

</style>