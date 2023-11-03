<template>
  <div class="q-pa-md row items-start q-gutter-sm">
    <q-card class="my-card text-white" style="background: teal">
      <div align="center" class="text-subtitle2 q-pa-md">
        This is your Interior Desires number.
      </div>
      <div align="center" class="text-subtitle2 q-pa-md">
        They determine what we desire from our physical plane.<br />This number
        describes our secret desires hidden inside our unconscious.<br />
        It is the vibration most close to our ego.
      </div>
      <q-card-section align="center">
        <q-input
          style="max-width: 300px"
          rounded
          outlined
          color="blue-grey-11"
          v-model="name"
          label="Enter your name"
          @keyup.enter="calculateInteriorDesiresCalculator"
        />
      </q-card-section>

      <q-separator inset />

      <q-card-section align="right">
        <q-btn
          class="text-white"
          :ripple="{ center: true }"
          color="secondary"
          label="Calculate"
          @click="calculateInteriorDesiresCalculator"
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
        v-if="numberDescriptions"
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
  j: 1,
  s: 1,
  b: 2,
  k: 2,
  t: 2,
  c: 3,
  l: 3,
  d: 4,
  m: 4,
  v: 4,
  n: 5,
  w: 5,
  f: 6,
  x: 6,
  g: 7,
  p: 7,
  y: 7,
  h: 8,
  q: 8,
  z: 8,
  r: 9,
};

const calculateInteriorDesiresCalculator = () => {
  let sum = 0;
  const cleanedName = name.value.replace(/\s+/g, "").toLowerCase();

  for (const char of cleanedName) {
    if (!"aeiou".includes(char)) {
      sum += numerologyMap[char] || 0;
    }
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
//   calculateInteriorDesiresCalculator,
//   numberDescriptions,
// };
</script>

<style></style>
