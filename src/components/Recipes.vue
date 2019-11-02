<template>
<div class="recipes">
    <div class="card mb-3" style="max-width:25rem">
        <div class="card-body">
            <h5 class="card-title">{{recipe.strMeal}}</h5>
            <h6 class="card-subtitle text-muted">{{recipe.strCategory}}</h6>
        </div>
        <img style="height: 30%; width: 100%;" :src= "recipe.strMealThumb" alt="Recipe image">
        <div class="card-body">
            <br>
            <h6 class="card-subtitle mb-2 text-muted">origin:{{recipe.strArea}}</h6>
        </div>
            <!-- <ol type="1" class="list-group list-group-flush" v-for="ingredient in recipe.ingredients">
                <li class="list-group-item">{{ingredient}}</li>
            </ol> -->

    </div>

</div>

    
</template>

<script>
    export default {
        name: 'Recipe',
        props: ['recipe'],
    }
</script>

<style>
</style>