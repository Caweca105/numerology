<template>
  <div>
    <AppHeader />
  </div>
  <div id="app">
    <div align="center" class="q-pa-md row items-start q-gutter-md">
      <MotivationCalculator class="col" ref="motivationRef" />
      <ExpressionCalculator class="col" ref="expressionRef" />
      <InteriorDesiresCalculator class="col" ref="interiorDesiresRef" />

      <!-- <q-btn
      class="text-white"
      :ripple="{ center: true }"
      color="secondary"
      label="Calculate All"
      @click="calculateAll"
    /> -->
    </div>

    <div class="q-pa-md row items-start q-gutter-md">
      <HouseNumber class="col" ref="houseNumberRef" />
    </div>
  </div>
  <div>
    <AppFooter />
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
