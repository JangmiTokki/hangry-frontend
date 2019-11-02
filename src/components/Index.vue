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
  
      // axios.get("https://www.themealdb.com/api/json/v1/1/search.php?f=" + this.searchTerm)
      axios.get("https://www.themealdb.com/api/json/v1/1/search.php?f=a")
      .then(response => {console.log(response); return response})
      .then(response => response.data.meals.map(recipe => {

        this.ingredients = this.getIngredients(recipe)
        const ingredientList={ingredients : this.ingredients}
        const recipes =  {...recipe, ...ingredientList}
        this.recipeList = [...this.recipeList, recipes]
      }))
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


