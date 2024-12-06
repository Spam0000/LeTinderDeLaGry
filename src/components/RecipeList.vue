<template>
    <div class="recipe-list">
      <!-- Itère sur les recettes pour afficher une carte pour chacune -->
      <RecipeMainCard
        v-for="(recipe, index) in recipes"
        :key="index"
        :recipe="recipe"
        @like-recipe="handleLikeRecipe"
        @adore-recipe="handleAdoreRecipe"
        @reject-recipe="handleRejectRecipe"
      />
    </div>
  </template>
  
  <script>
  // Importation du composant enfant
  import RecipeMainCard from "@/components/RecipeMainCard.vue";
  // Importation des données JSON
  import recipesData from "@/data/recipes.json";
  
  export default {
    name: "RecipeList",
    components: {
      RecipeMainCard, // Déclare RecipeMainCard comme composant enfant
    },
    data() {
      return {
        recipes: recipesData, // Charge les recettes depuis le fichier JSON
      };
    },
    methods: {
      handleLikeRecipe(recipe) {
        console.log("Recette aimée :", recipe.name); // Exemple de traitement
      },
      handleAdoreRecipe(recipe) {
        console.log("Recette adorée :", recipe.name); // Exemple de traitement
      },
      handleRejectRecipe(recipe) {
        console.log("Recette rejetée :", recipe.name); // Exemple de traitement
      },
    },
  };
  </script>
  
  <style scoped>
  .recipe-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
    margin: 20px;
  }
  </style>
  