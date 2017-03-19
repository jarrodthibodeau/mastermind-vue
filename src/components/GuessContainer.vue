<template>
    <div>
        <div class="contain">
            <div class="main">
                <div class="guess-container">
                    <GameButton v-for="guess in guesses" class="fill-in guess-button" :class="{'fade-out': isClearing}" :color="guess"/>
                </div>

                <div class="status-container"> 
                    <div class="status" v-for="status in statuses">  
                        <span v-if="status === 1" class="check"> &check; </span>
                        <span v-else-if="status === 0"> &harr; </span>
                        <span v-else> X </span> 
                    </div>
                 </div>   
             </div>

            <div class="selection-container">
                <span class="option" @click="submit(guesses)"> SUBMIT </span>
                <span class="option" @click="clear()"> CLEAR </span>
                <span class="option" @click="replay()"> REPLAY </span>
            </div>
        </div>
    </div>
    
</template>

<script>
    import GameButton from './GameButton'

    export default {
        name: 'GuessContainer',
        props: ['guesses', 'clear', 'submit', 'isClearing', 'statuses', 'replay'],
        components: {
            GameButton
        }
    }

</script>

<style>

    .guess-button {
        width: 14%;
        margin-left: 5%;
        margin-top: 3%;
        left: 0%;
    }

    .main {
        display : flex;
        width: 100%;
        justify-content: center;
        align-items: center;
        flex-flow: column;
    }

    .guess-container {
        display: flex;
        align-items: center;
        width: 75%;
        height: 175px;
        background-color: grey;
        border: 3px solid black;
        border-radius: 60px;
    }

    .contain {
        display: flex;
        flex-direction: row;
        justify-content: center;
        width: 100%;
    }
    
    .selection-container {
        position: relative;
        margin-left: 10%;
        display: flex;
        flex-direction: column;
        right: 20%;
        width: 30%;
    }

    .status-container {
        display:flex;
        flex-flow: row wrap;
        justify-content: space-between;
        width: 55%;
        position: relative;
    }

    .status {
        font-size: 1.75em;
        margin-top: 3%;
    }

    .option {
        font-size: 2.5em;
        margin-top: 1%;
    }

    .option:hover {
        cursor: pointer;
    }

    .check {
        color: green;
    }

    .fill-in {
        animation: fill-in .25s 1 ease-in forwards;
    }

    .fade-out {
        animation: fill-out .25s 1 ease-in forwards;
    }

    @keyframes fill-in {
        from {
            transform: scale(0);
        } to {
            transform: scale(1);
        }
    }

    @keyframes fill-out {
        from {
            transform: scale(1);
        } to {
            transform: scale(0);
        }
    }

    /* MEDIA QUERIES */

    
    @media screen and (max-width: 1399px) {
        .option {
            font-size: 2em;
        }
    }
    

     @media screen and (max-width: 900px) {
        .guess-container {
            width: 95%;

        }

        .selection-container {
            right: 10%;
            margin-top: 1%;
        }

        .status-container {
            width: 75%;
            margin-bottom: 3%;
        }

        .option {
            font-size: 2em;
            margin-left: 25%;
        }
    }

    @media screen and (max-width: 600px) {
        .guess-button {
            height: 50px;
            width: 9%;
            left: 3%;
        }

        .guess-container {
            width: 100%;
            height: 125px;
        }

        .selection-container {
            margin-top: 0%;
        }
    }

    @media screen and (max-width: 500px) {
        .guess-button {
            width: 7.5%;
            height: 45px;
            left: 2%;
        }

        .guess-container {
            width: 100%;
            height: 100px;
        }

        .selection-container {
            margin-top : 1%;
            right: 7%;
        }

        .option {
            font-size: 1.5em;
        }
    }

</style>