<template>
    <div class="card-button">
        <button v-on:click="addToCart" class="add-item">Add to Cart</button>
    </div>
</template>

<script>

    import { EventBus } from './event-bus.js';


    export default {
        name: "CardButtons",
        data() {
            return {
                cart: 0
            }
        },
        methods: {
            addToCart() {
                this.cart++;
                EventBus.$emit('add-to-cart', this.cart);
            }
        }
    }

</script>



<style scoped lang="scss">

    .card-button {
        margin-top:20px;

        button {
            font-size:12px;
            color: white;
            padding:10px;
            border: none;

            &.add-item {
                background-color:#42b983;
                &:hover{
                    background-color: orange;
                }
            }
        }
    }


</style>