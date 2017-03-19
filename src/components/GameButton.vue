<template>

    <div class="button" :style="{'background-color': color}" @click="guess(color)"> </div>

</template>

<script>

    export default {
        name: 'GameButton',
        props: ['color', 'guess']
    };

</script>

<style>
    .button {
        position: relative;
        width: 6%;
        right: 15.5%;
        height: 75px;
        border: 5px solid black;
        border-radius: 50%;
        margin: 30px;
        margin-top: -20px;
        transition: all .25s;
        box-shadow: 0 10px black;
        z-index: 1;
    }

    .button:hover {
        cursor: pointer;
        transform: rotateX(30deg);
    }

    .button:active {
        box-shadow: 0 0;
    }

    @media screen and (max-width: 1399px) {
        .button {
            width: 5%;
            height: 80px;
        }
    }

    @media screen and (max-width: 900px) {
        .button {
            width: 10%;
            left: 0%;
        }
    }

    @media screen and (max-width: 600px) {
        .button {
            width: 9%;
            height: 66px;
        }
    }

</style>



