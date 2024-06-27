<template>
  <div class="meal-item">
    <h4>{{ mealName }}</h4>
    <div class="meal-content">
      <img
        :src="`https://spoonacular.com/recipeImages/${meal.id}-556x370.${meal.imageType}`"
        :alt="meal.title"
      />
      <h5>{{ meal.title }}</h5>
      <p>Ready in {{ meal.readyInMinutes }} minutes</p>
      <p>{{ meal.servings }} Servings</p>
      <a :href="meal.sourceUrl" target="_blank">View Recipe</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    meal: Object,
    mealName: String,
  },
};
</script>

<style scoped></style>
