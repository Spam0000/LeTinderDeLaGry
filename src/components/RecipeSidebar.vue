<template>
  <div class="sidebar">
    <h2>Mes Recettes</h2>
    <ul class="recipe-list">
      <li
        v-for="(recipe, index) in favorites"
        :key="index"
        class="recipe-item"
        @click="$emit('set-current', recipe)"
      >
        <img :src="recipe.image" :alt="recipe.name" />
        <span>{{ recipe.name }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "RecipeSidebar",
  props: {
    favorites: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.sidebar {
  width: 25%;
  background: #1e1e1e;
  padding: 20px;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.5);
  overflow-y: auto; 
}

.sidebar h2 {
  margin: 0 0 20px 0;
  font-size: 24px;
}

.recipe-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.recipe-item {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
  padding: 10px;
  background: #2c2c2c;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s;
}

.recipe-item:hover {
  background: #3a3a3a;
}

.recipe-item img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.recipe-item span {
  font-size: 18px;
  color: white;
}

@media (max-width: 768px) {
  .sidebar {
    width: 100%;
    height: auto;
  }
}
</style>
