<template>
  <div class="card">
    <img :src="getImagePath(recipe.image)" :alt="recipe.name" class="recipe-image" />
    <h1 class="recipe-title">{{ recipe.name }}</h1>
    <p class="recipe-description">{{ recipe.description }}</p>
    <div class="actions">
      <button class="like-btn" @click="$emit('like-recipe', recipe)">
        <img src="@/assets/logo/heart.png" alt="Aimer" />
      </button>
      <button class="adore-btn" @click="$emit('adore-recipe', recipe)">
        <img src="@/assets/logo/star.png" alt="Favoris" />
      </button>
      <button class="reject-btn" @click="$emit('reject-recipe')">
        <img src="@/assets/logo/cross.png" alt="Rejeter" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      required: true,
    },
  },
  methods: {
    getImagePath(image) {
      try {
        return require(`@/assets/recipe/${image}`);
      } catch (err) {
        console.error("Image introuvable :", image);
        return require("@/assets/recipe/placeholder.jpg"); // Placeholder si image introuvable
      }
    },
  },
};
</script>

<style scoped>
.card {
  background: #1e1e1e;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3);
  text-align: center;
  width: 100%;
  max-width: 400px;
  margin: auto;
}

.recipe-image {
  width: 100%;
  border-radius: 10px;
  margin-bottom: 20px;
}

.recipe-title {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #fff;
}

.recipe-description {
  font-size: 16px;
  line-height: 1.5;
  margin-bottom: 20px;
  color: #ccc;
}

.actions {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.actions button {
  background: white;
  border: none;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.2);
  transition: transform 0.2s ease;
}

.actions button:hover {
  transform: scale(1.1);
}

.actions img {
  width: 30px;
  height: 30px;
}
</style>
