<template>
<div id="attempts">
    <h1> Guesses </h1>
        <hr> </hr>
    <div v-for="(attempt, index) in attempts" class="attempt-row">
        {{index + 1}}. <div v-for="color in attempt">
            <div class="mini-button" :style="{'background-color': color}"> </div>
        </div>
    </div>
</div>
</template>

<script>
    export default {
        name: 'Guesses',
        props: ['attempts']
    }
</script>

<style>

    #attempts {
        position: relative;
        bottom: 10%;
    }

    .mini-button {
        height: 25px;
        width: 25px;
        border-radius: 50%;
        border: 3px dotted black;
        margin-left: 10px;
    }

    .attempt-row {
        display: flex;
        justify-content: center;
        margin-top: 10px;
        width: 0%;
    }

    @media screen and (max-width: 900px) {
        .mini-button {
            width: 50px;
            height: 50px;
        }
    }
</style>