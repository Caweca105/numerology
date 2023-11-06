<template>
  <div class="q-pa-md items-start q-gutter-sm">
    <q-card class="my-card text-white fixed-size-card" style="background: teal">
      <div align="center" class="text-subtitle2 q-pa-md">
        This is your House number.
      </div>
      <div align="center" class="text-subtitle2 q-pa-md">
        It describes your house natural powers.
      </div>
      <q-card-section align="center">
        <q-input
          style="width: 300px"
          rounded
          outlined
          color="blue-grey-11"
          v-model="name"
          label="Enter your house number"
          @keyup.enter="calculateHouseNumberCalculator"
        />
      </q-card-section>

      <q-separator inset />

      <q-card-section align="right">
        <q-btn
          class="text-white"
          :ripple="{ center: true }"
          color="secondary"
          label="Calculate"
          @click="calculateHouseNumberCalculator"
        />
      </q-card-section>

      <q-separator v-if="totalValue" inset />

      <div
        align="center"
        class="text-subtitle2 q-pa-md"
        v-if="totalValue"
        :key="totalValue"
      >
        Your house number is: {{ totalValue }}
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
};

const numberDescription = computed(() => {
  return numberDescriptions[totalValue.value] || "";
});

const calculateHouseNumberCalculator = () => {
  let number = parseInt(name.value, 10);
  let sum = number;

  // Continue reducing the number until it's a single-digit number
  while (sum >= 10) {
    let tempSum = 0;
    const digits = sum.toString().split("").map(Number); // Extract digits from the number

    for (const digit of digits) {
      tempSum += digit;
    }
    sum = tempSum;
  }

  totalValue.value = sum;
};
</script>

<style>
.fixed-size-card {
  width: 400px;
  height: 300px;
}
</style>
