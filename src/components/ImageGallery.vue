<template>
    <div :class="{ gallery: isVisible }">
        <h1> {{ category }}</h1>
      <div class="gallery-wrapper">
          <div class="gallery-wrapper__card" v-for="item in books" :key="item['id']">
              <img :src="item.volumeInfo.imageLinks.thumbnail" class="gallery-wrapper__card__thumb" alt="">
              <h2>{{ item.volumeInfo.title }}</h2>
              <h3>{{ item.volumeInfo.authors[0] }}</h3>
              <CardButtons />
          </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios'
import CardButtons from './CardButtons.vue'
import { EventBus } from './event-bus.js'

export default {
    components: {
        CardButtons
    },
    data() {
        return {
            books: [],
            loading: true,
            cart: 0,
            category: 'sports',
            isVisible: 'false'
        }
    },
    methods: {
        selectedCategory(data) {
            this.category = data
            let cat = 'https://www.googleapis.com/books/v1/volumes?q=' + data;
            axios
                .get(cat)
                .then(response => (this.books = response.data.items))
        },
    }  ,
        mounted() {
            let cat = 'https://www.googleapis.com/books/v1/volumes?q=' + this.category;

            axios
                .get(cat)
                .then(response => (this.books = response.data.items))

        },
        created() {
            EventBus.$on('category', (data) => {
                this.selectedCategory(data);
            }),
            EventBus.$on('isVisible', (data) => {
                    this.isVisible=data;
                })
        },
    }


</script>

<style lang="scss" scoped>

$font-size-h2: 15px;
$font-size-h3: 0.82*$font-size-h2;
$width: 30%;
$margin-top: 10%;

.gallery{
    padding-top:130px;
}

h1 {
    color:#35495d;
    font-size:30px;
    border-bottom: 2px solid green;
    display: inline-block;
}

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