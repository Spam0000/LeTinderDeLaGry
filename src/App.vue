<template>
  <div id="app">
    <div class="container">
      <!-- Barre des favoris -->
      <div class="favorites">
        <!-- Section des Favoris -->
        <div class="favorites-header">
          <h2>Favoris</h2>
        </div>
        <div class="favorites-content">
          <ul>
            <li v-for="(favorite, index) in favorites" :key="index">
              <img :src="getImagePath(favorite.image)" :alt="favorite.name" class="favorite-image" />
              <p>{{ favorite.name }}</p>
            </li>
          </ul>
        </div>

        <!-- Section des Aimés -->
        <div class="liked-header">
          <h2>Aimé(e)s</h2>
        </div>
        <div class="liked-content">
          <ul>
            <li v-for="(liked, index) in liked" :key="index">
              <img :src="getImagePath(liked.image)" :alt="liked.name" class="favorite-image" />
              <p>{{ liked.name }}</p>
            </li>
          </ul>
        </div>
      </div>

      <!-- Carte principale -->
      <div class="main-card">
        <RecipeMainCard
          :recipe="currentRecipe"
          @like-recipe="addToLiked"
          @adore-recipe="addToFavorites"
          @reject-recipe="nextRecipe"
        />
      </div>
    </div>
  </div>
</template>

<script>
import RecipeMainCard from "@/components/RecipeMainCard.vue";
import recipesData from "@/data/recipes.json";

export default {
  name: "App",
  components: {
    RecipeMainCard,
  },
  data() {
    return {
      recipes: [...recipesData], // Toutes les recettes
      favorites: [], // Liste des favoris
      liked: [], // Liste des recettes aimées
      currentIndex: 0, // Index de la recette actuelle
    };
  },
  computed: {
    currentRecipe() {
      // Retourne la recette actuellement affichée
      return this.recipes[this.currentIndex];
    },
  },
  methods: {
    getImagePath(image) {
      try {
        return require(`@/assets/recipe/${image}`);
      } catch (err) {
        console.error("Image introuvable :", image);
        return require("@/assets/recipe/placeholder.jpg");
      }
    },
    addToFavorites(recipe) {
      if (!this.favorites.some((fav) => fav.name === recipe.name)) {
        this.favorites.push(recipe);
      }
      this.nextRecipe();
    },
    addToLiked(recipe) {
      if (!this.liked.some((like) => like.name === recipe.name)) {
        this.liked.push(recipe);
      }
      this.nextRecipe();
    },
    nextRecipe() {
      if (this.currentIndex < this.recipes.length - 1) {
        this.currentIndex++;
      } else {
        alert("Vous avez vu toutes les recettes !");
      }
    },
  },
};
</script>

<style scoped>
/* Conteneur principal */
.container {
  display: flex;
  height: 100vh;
  width: 100vw;
}

/* Barre des favoris */
.favorites {
  width: 33.33%;
  background-color: #f8f9fa;
  display: flex;
  flex-direction: column;
  border-right: 1px solid #ddd;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  overflow-y: auto;
}

/* Section des Favoris */
.favorites-header {
  background-color: #e9ecef;
  padding: 10px 20px;
  border-bottom: 1px solid #ccc;
}

.favorites-header h2 {
  margin: 0;
  font-size: 18px;
  text-align: center;
}

.favorites-content {
  padding: 10px 20px;
}

/* Section des Aimés */
.liked-header {
  background-color: #e9ecef;
  padding: 10px 20px;
  border-top: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}

.liked-header h2 {
  margin: 0;
  font-size: 18px;
  text-align: center;
}

.liked-content {
  padding: 10px 20px;
}

/* Images et listes */
.favorites-content ul,
.liked-content ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.favorites-content li,
.liked-content li {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.favorite-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

/* Carte principale */
.main-card {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}
</style>
