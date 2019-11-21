<template>
    <div>
        <nav>
            <div>
                <img alt="Vue logo" src=".././assets/logo.png" height="30px">
            </div>

            <div>
                <ul>
                    <li><a href="#">Home</a></li>
                    <li><a href="#" v-on:click="filterVisible">Categories</a></li>
                    <li><a href="#">About Us</a></li>
                </ul>
            </div>
            <div>
                <Cart />
            </div>
        </nav>
        <div class="filter" :class="{ visible: visible }">
            <ul>
                <li><a href="#" v-on:click="chooseCategory('Sports')">Sports</a></li>
                <li><a href="#" v-on:click="chooseCategory('Food')">Food</a></li>
            </ul>
        </div>
    </div>
</template>

<script>
    import Cart from './Cart.vue';
    import { EventBus } from './event-bus.js';

    export default {
        name: "Nav",
        components: {
                Cart
            },
        methods: {
            filterVisible() {
                this.visible = !this.visible;
                EventBus.$emit('isVisible', this.visible);
            },
            chooseCategory(category) {
                window.console.log(category)
                this.category = category
                    EventBus.$emit('category', this.category);
            }
        },
        data() {
            return {
                visible: false,
                category: 'sports'

            }
        },
        }

</script>

<style scoped lang="scss">

    nav {
        display:flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        height: 60px;
        margin:0px;
        top:0;
        width: 100%;
        background-color: #f2f7ed;
        position:fixed;
        z-index: 3;


        div {
            display: flex;
            height: 100%;
            align-items: center;

            &:nth-child(1) {
                width: 300px;
                margin-left: 30px;

            }

            &:nth-child(2) {
                justify-self: center;
                margin: 0px;
            }

            &:nth-child(3) {
                width: 300px;
                margin-right: 30px;
            }
        }



        ul {
            list-style-type: none;
            margin: 0px;
            padding: 0px;

            li {
                display:inline;
                margin:0px 30px;

                @media screen and (max-width: 600px) {
                    margin:0px 10px;
                    font-size: 13px;
                }
            }

            a {
                text-transform: uppercase;
                letter-spacing: 0.8px;
                font-weight: bold;
                text-decoration: none;
                color:#35495d;

                &:hover {
                    color:green;
                }
            }
        }
    }


    .filter {
        display: flex;
        position: fixed;
        flex-flow: row wrap;
        width:100%;
        height: 40px;
        margin: auto;
        justify-content: center;
        align-content: center;
        align-items: center;
        background-color: #35495d;
        transform: translateY(-80px);
        transition: ease-in-out 0.5s;
        z-index: 1;


        ul {
            width: 300px;
            list-style: none;
            padding: 0px;

            li {
                display:inline;
                margin: 0px 20px;
            }

            a {
                color: white;
                text-transform: uppercase;
                font-size: 13px;
                text-decoration: none;
            }
        }

        &.visible {
           transform: translateY(0px);

        }

    }

</style>