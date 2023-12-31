<template>
  <div class="q-pa-md items-start q-gutter-sm">
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
          :rules="rules"
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

      <q-separator v-if="totalDesiresValue" inset />

      <div
        align="center"
        class="text-subtitle2 q-pa-md"
        v-if="totalDesiresValue"
        :key="totalDesiresValue"
      >
        Your numerology number is: {{ totalDesiresValue }}
      </div>
      <div
        align="center"
        class="text-subtitle2 q-pa-md"
        v-if="numberDescriptionDesires"
      >
        {{ numberDescriptionDesires }}
      </div>
    </q-card>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const name = ref("");
const totalDesiresValue = ref(0);

const numberDescriptionDesiress = {
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

const numberDescriptionDesires = computed(() => {
  return numberDescriptionDesiress[totalDesiresValue.value] || "";
});

const onlyLettersRule = (val) =>
  /^[A-Za-z\u00C0-\u00FF\s]+$/.test(val) || "Only letters are allowed";

const rules = [onlyLettersRule];

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
    totalDesiresValue.value = sum;
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

  totalDesiresValue.value = sum;
};

// return {
//   name,
//   totalDesiresValue,
//   numberDescriptionDesires,
//   calculateInteriorDesiresCalculator,
//   numberDescriptionDesiress,
// };
</script>

<style></style>
