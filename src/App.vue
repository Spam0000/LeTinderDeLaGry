<template>
  <div class="app">
    <RecipeSidebar :favorites="favorites" @set-current="setCurrentRecipe" />
    <RecipeMainCard :recipe="currentRecipe" @add-to-favorites="addToFavorites" />
  </div>
</template>

<script>
import RecipeSidebar from "./components/RecipeSidebar.vue";
import RecipeMainCard from "./components/RecipeMainCard.vue";
import recipesData from "./data/recipes.json"; 

export default {
  components: {
    RecipeSidebar,
    RecipeMainCard,
  },
  data() {
    return {
      currentRecipe: recipesData[0],
      favorites: [],
      recipes: recipesData,
    };
  },
  methods: {
    addToFavorites(recipe) {
      if (!this.favorites.find((r) => r.name === recipe.name)) {
        this.favorites.push(recipe);
      }
    },
    setCurrentRecipe(recipe) {
      this.currentRecipe = recipe;
    },
  },
};
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 100vh;
}

@media (max-width: 768px) {
  .app {
    flex-direction: column; 
  }
}
</style>
