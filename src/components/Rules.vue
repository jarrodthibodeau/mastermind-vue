<template>
<div>
    <h1> Rules </h1>
    <hr/>
    <ul>
        <li> You must guess the correct combination of colors in 10 tries! </li>
        <li> Click the color of your choice to add it to the guess selection </li>
        <li> If you have guessed one of the columns correctly, a green &check; will appear </li>
        <li> If you selected a column in which the color is actually in another column a &harr; will appear </li>
        <li> Remember, there can be multiple of the same color </li>
    </ul>
</div>
</template>


<script>
    export default {
        name: 'Rules'
    }
</script>


<style> 
    ul  {
        list-style-type: square;
        list-style-position: outside
    }
    
    @media screen and (max-width: 900px) {
        #rules {
            margin-top: 5%;
        }
    }
    
</style>