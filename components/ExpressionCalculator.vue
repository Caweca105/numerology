<template>
  <div class="q-pa-md items-start q-gutter-sm">
    <q-card class="my-card text-white fixed-size-card" style="background: teal">
      <div align="center" class="text-subtitle2 q-pa-md">
        This is your Expression number.
      </div>
      <div align="center" class="text-subtitle2 q-pa-md">
        It describes your natural talents and abilities and <br />how you can
        best take advantage of them to get the most out of life.
      </div>
      <q-card-section align="center">
        <q-input
          style="max-width: 300px"
          rounded
          outlined
          color="blue-grey-11"
          v-model="name"
          label="Enter your name"
          @keyup.enter="calculateExpressionCalculator"
        />
      </q-card-section>

      <q-separator inset />

      <q-card-section align="right">
        <q-btn
          class="text-white"
          :ripple="{ center: true }"
          color="secondary"
          label="Calculate"
          @click="calculateExpressionCalculator"
        />
      </q-card-section>

      <q-separator v-if="totalValue" inset />

      <div
        align="center"
        class="text-subtitle2 q-pa-md"
        v-if="totalValue"
        :key="totalValue"
      >
        Your numerology number is: {{ totalValue }}
      </div>
      <div
        align="center"
        class="text-subtitle2 q-pa-md"
        v-if="numberDescription"
      >
        {{ numberDescription }}
      </div>
    </q-card>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const name = ref("");
const totalValue = ref(0);

const numberDescriptions = {
  1: "This is the description for number 1.",
  2: "This is the description for number 2.",
  3: "This is the description for number 3.",
  4: "This is the description for number 4.",
  5: "This is the description for number 5.",
  6: "This is the description for number 6.",
  7: "This is the description for number 7.",
  8: "This is the description for number 8.",
  9: "This is the description for number 9.",
  11: "This is the description for master number 11.",
  22: "This is the description for master number 22.",
};

const numberDescription = computed(() => {
  return numberDescriptions[totalValue.value] || "";
});

const numerologyMap = {
  a: 1,
  j: 1,
  s: 1,
  b: 2,
  k: 2,
  t: 2,
  c: 3,
  l: 3,
  u: 3,
  d: 4,
  m: 4,
  v: 4,
  e: 5,
  n: 5,
  w: 5,
  f: 6,
  o: 6,
  x: 6,
  g: 7,
  p: 7,
  y: 7,
  h: 8,
  q: 8,
  z: 8,
  i: 9,
  r: 9,
};

const calculateExpressionCalculator = () => {
  let sum = 0;
  const cleanedName = name.value.replace(/\s+/g, "").toLowerCase();

  for (const char of cleanedName) {
    sum += numerologyMap[char] || 0;
  }

  // Check for master numbers 11 and 22
  if (sum === 11 || sum === 22) {
    totalValue.value = sum;
    return;
  }

  // Reduce to a single digit number if not a master number
  while (sum >= 10) {
    let tempSum = 0;
    const digits = sum.toString().split("").map(Number);
    for (const digit of digits) {
      tempSum += digit;
    }
    sum = tempSum;

    // Again check for master numbers after reducing
    if (sum === 11 || sum === 22) {
      break;
    }
  }

  totalValue.value = sum;
};

// return {
//   name,
//   totalValue,
//   numberDescription,
//   calculateExpressionCalculator,
//   numberDescriptions,
// };
</script>

<style>
.fixed-size-card {
  width: 400px;
  height: 300px;
}
</style>
