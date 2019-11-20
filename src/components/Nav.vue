<template>
    <nav>
        <div>
            <img alt="Vue logo" src=".././assets/logo.png" height="30px">
        </div>

        <div>
            <ul>
                <li>Home</li>
                <li>Books</li>
                <li>About Us</li>
            </ul>
        </div>
        <div>
            <Cart />
        </div>
    </nav>
</template>

<script>
    import Cart from './Cart.vue';

    export default {
        name: "Nav",
        components: {
                Cart
            }
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
            text-transform: uppercase;
            letter-spacing: 0.8px;
            font-weight: bold;

            li {
                display:inline;
                margin:0px 30px;

                @media screen and (max-width: 600px) {
                    margin:0px 10px;
                    font-size: 13px;
                }

            }


        }
    }

</style>