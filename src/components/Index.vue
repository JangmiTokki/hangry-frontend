<template>
  <div class="index">
    <Header/>
    <Search @updateSearchTerm="updateSearchTerm" :searchTerm="searchTerm"/>
    <div class="recipe-container">
      <div class="recipe-cards">
        <ul v-for="recipe in recipeList"><Recipes :recipe="recipe"/></ul>
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
  import Recipes from '../components/Recipes.vue'
  import Header from '../components/Header.vue'
  import Search from '../components/Search.vue'
export default {
  name: 'Index',
  components: {
    Recipes,
    Header,
    Search
  },
  data: function(){
    return {
      recipeList: [],
      ingredients: [],
      searchTerm: ''
    }
  },
  mounted(){
    this.getRecipes()
  },
  methods: {
    getIngredients(recipe){
      const recipeKeys = Object.keys(recipe)
      const ingredientKeys = recipeKeys.filter(key => {
        return key.includes("strIngredient")
      })
      const ingredients = ingredientKeys.map(key => {
        return recipe[key]
      })
      return ingredients.filter(ingredient => ingredient) 
    },
    updateSearchTerm(searchTerm){
      this.searchTerm = searchTerm
      this.getRecipes()
    },
    getRecipes(){
      axios.get("https://www.themealdb.com/api/json/v1/1/search.php?s=" + this.searchTerm)
      .then(response => {
  
        const meals = response.data.meals || []

        return meals.map(recipe => {
          this.ingredients = this.getIngredients(recipe)
          const ingredientList={ingredients : this.ingredients}
          const recipeWithIngredients =  {...recipe, ...ingredientList}
          return recipeWithIngredients
        })
      })
      .then(recipesWithIngredients => {this.recipeList = recipesWithIngredients})
    }
  },
   
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .recipe-cards{
    display: grid;
    grid-gap: 0.5rem;
    grid-template-columns: repeat(3, 25rem)
  }
</style>


