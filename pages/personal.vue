<template>
  <div class="q-pa-md items-start q-gutter-sm">
    <q-card class="my-card text-white" style="background: teal">
      <div align="center" class="text-subtitle2 q-pa-md">
        <strong>This is your Personal numbers calculator.</strong>
      </div>
      <div align="center" class="text-subtitle2 q-pa-md">
        It describes stuff.
      </div>
      <!-- Input Field -->
      <q-card-section align="center">
        <q-input
          style="max-width: 300px"
          rounded
          outlined
          color="blue-grey-11"
          label="Enter your name"
          v-model="name"
          @keyup.enter="calculateNumerology"
        />
      </q-card-section>

      <q-separator inset />

      <!-- Calculate Button -->
      <q-card-section align="right">
        <q-btn
          class="text-white"
          :ripple="{ center: true }"
          color="secondary"
          label="Calculate"
          @click="calculateNumerology"
        />
      </q-card-section>

      <!-- Results Section -->
      <q-separator v-if="resultsAvailable" inset />

      <div v-if="resultsAvailable">
        <div align="center" class="text-subtitle2 q-pa-md">
          Interior Desires number: {{ totalDesiresValue }}
          <br />
          {{ numberDescriptionDesires }}
        </div>

        <div align="center" class="text-subtitle2 q-pa-md">
          Motivation number: {{ totalMotivationValue }}
          <br />
          {{ numberDescriptionMotivation }}
        </div>

        <div align="center" class="text-subtitle2 q-pa-md">
          Expression number: {{ totalExpressionValue }}
          <br />
          {{ numberDescriptionExpression }}
        </div>
      </div>
    </q-card>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const name = ref("");
const totalDesiresValue = ref(0);
const totalMotivationValue = ref(0);
const totalExpressionValue = ref(0);

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

const numberDescriptionMotivations = {
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
const numberDescriptionExpressions = {
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

const numberDescriptionDesires = computed(
  () => numberDescriptionDesiress[totalDesiresValue.value] || ""
);

const numberDescriptionMotivation = computed(
  () => numberDescriptionMotivations[totalMotivationValue.value] || ""
);

const numberDescriptionExpression = computed(
  () => numberDescriptionExpressions[totalExpressionValue.value] || ""
);

const onlyLettersRule = (val) =>
  /^[A-Za-z\u00C0-\u00FF\s]+$/.test(val) || "Only letters are allowed";

const rules = [onlyLettersRule];

const numerologyMap = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  e: 5,
  f: 6,
  g: 7,
  h: 8,
  i: 9,
  j: 1,
  k: 2,
  l: 3,
  m: 4,
  n: 5,
  o: 6,
  p: 7,
  q: 8,
  r: 9,
  s: 1,
  t: 2,
  u: 3,
  v: 4,
  w: 5,
  x: 6,
  y: 7,
  z: 8,
};

const calculateNumerology = () => {
  let sumDesires = 0,
    sumMotivation = 0,
    sumExpression = 0;
  const cleanedName = name.value.replace(/\s+/g, "").toLowerCase();

  for (const char of cleanedName) {
    const charValue = numerologyMap[char] || 0;

    // Logic for Interior Desires (Consonants)
    if (!"aeiou".includes(char)) {
      sumDesires += charValue;
    }

    // Logic for Motivation (Vowels)
    if ("aeiou".includes(char)) {
      sumMotivation += charValue;
    }

    // Logic for Expression (All characters)
    sumExpression += charValue;
  }

  // Reduce each sum to a single digit or master number
  totalDesiresValue.value = reduceToSingleDigitOrMaster(sumDesires);
  totalMotivationValue.value = reduceToSingleDigitOrMaster(sumMotivation);
  totalExpressionValue.value = reduceToSingleDigitOrMaster(sumExpression);
};

const reduceToSingleDigitOrMaster = (sum) => {
  if (sum === 11 || sum === 22) return sum;
  while (sum >= 10) {
    sum = sum
      .toString()
      .split("")
      .map(Number)
      .reduce((a, b) => a + b, 0);
  }
  return sum;
};

const resultsAvailable = computed(
  () =>
    totalDesiresValue.value > 0 ||
    totalMotivationValue.value > 0 ||
    totalExpressionValue.value > 0
);
</script>
