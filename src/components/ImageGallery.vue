<template>
    <div class="custom-properties">
        <div class="gallery">
            <h1> {{ category }}</h1>

            <div class="input-container">
                <input type="text" placeholder="Type a title or author" v-model="bookSearchString" />
            </div>

          <div class="gallery__wrapper">
              <div class="gallery__card" v-for="item in filteredBookFeed" :key="item['id']">
                  <img :src="item.volumeInfo.imageLinks.thumbnail" class="gallery__thumb" alt="">
                  <h2>{{ item.volumeInfo.title }}</h2>
                  <h3>{{ item.volumeInfo.authors[0] }}</h3>
                  <CardButtons />
              </div>
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
            bookSearchString:'',
            loading: true,
            cart: 0,
            category: 'Sports',
            categoryIsVisible: 'false',

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
    },
    computed: {
        filteredBookFeed: function () {
            let books = this.books;
            let bookSearchString = this.bookSearchString;

            if(!bookSearchString){
                return books;
            }

            bookSearchString = bookSearchString.trim().toLowerCase();

            books = books.filter(function(item){

                if(item.volumeInfo.title.toLowerCase().indexOf(bookSearchString) !== -1){
                    return item;
                }
            })
            window.console.log(books)
            return books;
        }
    },

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
                    this.categoryIsVisible = data;
                    window.console.log(data)
                })
        }
    }



</script>

<style lang="scss" scoped>

    $font-size-h2: 15px;
    $font-size-h3: 0.82*$font-size-h2;
    $width: 30%;

    @media (max-width=500px) {

    }

    .custom-properties {
        --margin-top: 5%;
    }


    h1 {
        color:#35495d;
        font-size:30px;
        border-bottom: 2px solid green;
        display: inline-block;
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

    .input-container{
        margin: 30px auto;

        input {
            width:300px;
            height:20px;
            border: 1px solid lightgrey;
            border-radius: 20px;
            padding: 10px 30px;
            font-size: 15px;

            &:focus{
                outline: 1px white;
                outline-offset: 5px;
            }
        }
    }

    .gallery{
        padding-top: var(--margin-top);

        &__search {
            margin: 30px 0px;
        }

        &__wrapper {
            display: flex;
            width: 100%;
            flex-wrap: wrap;
            flex-direction: row;
            justify-content: center;
        }

        &__card {
            /*width: $width;*/
            flex: 1;
            min-width: 300px;
            background-color: #f1eeee;
            margin: 10px;
            padding: 15px 0px 15px 0px;

            &:hover {
                background-color: #e6e6e6;
            }
        }

        &__thumb{
            height:200px;
        }
    }


</style>