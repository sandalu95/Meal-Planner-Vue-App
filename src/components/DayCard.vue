<template>
  <div class="day-card">
    <div class="card">
      <p>{{ day.toUpperCase() }}</p>
      <hr />
      <div class="meals">
        <MealItem
          v-for="(meal, index) in meals"
          :key="index"
          :meal="meal"
          :mealName="mealNames[index]"
        />
      </div>
      <div class="nutrients">
        <p>{{ nutrients.calories }} kCal</p>
        <div>
          <p>Protein: {{ nutrients.protein }}g</p>
          <p>Fat: {{ nutrients.fat }}g</p>
          <p>Carbohydrates: {{ nutrients.carbohydrates }}g</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MealItem from "./MealItem.vue";

export default {
  props: {
    day: String,
    meals: Array,
    nutrients: Object,
  },
  components: {
    MealItem,
  },
  data() {
    return {
      mealNames: ["Breakfast", "Lunch", "Dinner"],
    };
  },
};
</script>

<style scoped></style>
