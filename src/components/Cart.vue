<template>
    <div class="cart">
        <div class="cart__icon"></div>
        <h3> {{ cart }} </h3>
    </div>
</template>

<script>
    import {EventBus} from './event-bus.js';

    export default {
        name: "Cart",

        data() {
            return {
                cart: 0,
            };
        },
        created() {
            EventBus.$on('add-to-cart', (data) => {
                this.cart = data;
            })
        }
    }
</script>

<style scoped lang="scss">

    .cart {
        justify-content: flex-end;

        &__icon {
            width: 40px;
            height: 100%;
            background-image: url('.././assets/cart.png');
            background-size: 25px;
            background-repeat: no-repeat;
            background-position: center center;
        }
    }

</style>