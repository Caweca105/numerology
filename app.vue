<template>
  <div id="app">
    <div class="text-h1 text-white" align="center">Numerology Calculator</div>
    <div align="center" class="q-pa-md row items-start q-gutter-md">
      <MotivationCalculator ref="motivationRef" />
      <ExpressionCalculator ref="expressionRef" />
      <InteriorDesiresCalculator ref="interiorDesiresRef" />
      <HouseNumber ref="houseNumberRef" />

      <!-- <q-btn
      class="text-white"
      :ripple="{ center: true }"
      color="secondary"
      label="Calculate All"
      @click="calculateAll"
    /> -->
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import ExpressionCalculator from "../components/ExpressionCalculator.vue";
import MotivationCalculator from "../components/MotivationCalculator.vue";
import InteriorDesiresCalculator from "../components/InteriorDesiresCalculator.vue";
import HouseNumber from "./components/HouseNumber.vue";

const expressionRef = ref(null);
const motivationRef = ref(null);
const interiorDesiresRef = ref(null);

// const calculateAll = () => {
//   expressionRef.value.calculateExpressionCalculator();
//   motivationRef.value.calculateMotivationCalculator();
//   interiorDesiresRef.value.calculateInteriorDesiresCalculator();
// };
</script>

<style>
#app {
  background-color: rgb(49, 49, 49);
}
</style>
