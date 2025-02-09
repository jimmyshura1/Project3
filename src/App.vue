<template>
  <div class="container">
    <h1>Recipe Builder</h1>
    <form @submit.prevent="submitRecipe">
      <label for="ingredients">Ingredients (separate by comma):</label>
      <textarea id="ingredients" v-model="ingredients" required></textarea>
      
      <label for="directions">Directions (each step on a new line):</label>
      <textarea id="directions" v-model="directions" required></textarea>
      
      <button type="submit">Generate Full Recipe</button>
    </form>
    
    <div v-if="recipe.ingredients.length" class="recipe-output">
      <h2>Ingredients</h2>
      <ul>
        <li v-for="(ingredient, index) in recipe.ingredients" :key="index">{{ ingredient }}</li>
      </ul>
      <h2>Directions</h2>
      <ul>
        <li v-for="(direction, index) in recipe.directions" :key="index">{{ direction }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const ingredients = ref('');
    const directions = ref('');
    const recipe = ref({ ingredients: [], directions: [] });
    
    const submitRecipe = () => {
      recipe.value.ingredients = ingredients.value.split(',').map(i => i.trim());
      recipe.value.directions = directions.value.split('\n').map(d => d.trim());
    };

    return { ingredients, directions, recipe, submitRecipe };
  }
};
</script>