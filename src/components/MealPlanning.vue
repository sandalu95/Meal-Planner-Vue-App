<template>
  <div class="container">
    <div>
      <div v-if="activeStep === 0">
        <p>Welcome to personalized meal planning!</p>
        <button @click="handleNext">Get Started!</button>
      </div>
      <div v-else-if="activeStep === 1">
        <form>
          <!-- Form Fields for Age, Gender, Weight, Height -->
        </form>
      </div>
      <!-- Other steps go here -->
      <div v-if="activeStep === 7">
        <p>Congratulations! Your personalized meal plan is ready.</p>
        <div v-if="generatedPlan" class="weekly-meal-plan">
          <DayCard
            v-for="(day, index) in generatedPlan.week"
            :key="index"
            :day="day"
            :meals="generatedPlan.week[day].meals"
            :nutrients="generatedPlan.week[day].nutrients"
          />
        </div>
      </div>
    </div>
    <div>
      <button @click="handleBack" :disabled="activeStep === 0">Back</button>
      <button @click="handleNext" :disabled="activeStep === 7">Next</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import DayCard from "./DayCard.vue";

export default {
  components: {
    DayCard,
  },
  data() {
    return {
      userInput: {
        age: "",
        gender: "",
        weight: "",
        height: "",
        activityLevel: "sedentary",
        diet: "No Diet",
        healthGoals: "weightLoss",
      },
      generatedPlan: null,
      activeStep: 0,
      selectedAllergies: [],
      recommendedCalorie: 0,
      calorieIntake: "",
    };
  },
  methods: {
    handleNext() {
      // Handle Next Step Logic
    },
    handleBack() {
      this.activeStep -= 1;
    },
    generateDietPlan() {
      const dailyCalories = this.calorieIntake || this.recommendedCalorie;
      const dietPreference =
        this.userInput.diet === "No Diet" ? "" : this.userInput.diet;

      axios
        .get(
          `https://api.spoonacular.com/mealplanner/generate?apiKey=YOUR_API_KEY&timeFrame=week&targetCalories=${dailyCalories}&diet=${dietPreference}&exclude=${this.selectedAllergies.join(
            ","
          )}`
        )
        .then((response) => {
          this.generatedPlan = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
