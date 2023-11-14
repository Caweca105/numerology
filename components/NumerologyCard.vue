<template>
  <div class="q-pa-md items-start q-gutter-sm">
    <q-card class="my-card text-white" style="background: teal">
      <!-- Input Field -->
      <q-card-section align="center">
        <q-input
          style="max-width: 300px"
          rounded
          outlined
          color="blue-grey-11"
          :rules="rules"
          label="Enter your name"
          v-model="name"
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
