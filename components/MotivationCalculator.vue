<template>
  <div class="q-pa-md items-start q-gutter-sm">
    <q-card class="my-card text-white" style="background: teal">
      <div align="center" class="text-subtitle2 q-pa-md">
        This is your Motivation number.
      </div>
      <div align="center" class="text-subtitle2 q-pa-md">
        It describes what you ant to be, to do, and to have in your life.
        <br />This number is what makes us advance <br />
        and motivate us in our lifes. It is the driving force behind our
        actions.
      </div>
      <q-card-section align="center">
        <q-input
          style="width: 300px"
          rounded
          outlined
          color="blue-grey-11"
          v-model="name"
          label="Enter your name"
          @keyup.enter="calculateMotivationCalculator"
        />
      </q-card-section>

      <q-separator inset />

      <q-card-section align="right">
        <q-btn
          class="text-white"
          :ripple="{ center: true }"
          color="secondary"
          label="Calculate"
          @click="calculateMotivationCalculator"
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
  a: 1,
  e: 5,
  i: 9,
  o: 6,
  u: 3,
};

const calculateMotivationCalculator = () => {
  let sum = 0;
  const cleanedName = name.value.replace(/\s+/g, "").toLowerCase();

  for (const char of cleanedName) {
    if ("aeiou".includes(char)) {
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
//   calculateMotivationCalculator,
//   numberDescriptions,
// };
</script>

<style></style>
