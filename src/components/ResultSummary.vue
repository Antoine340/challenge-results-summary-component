<script setup lang="ts">
import { computed } from 'vue'

export interface Result {
  category: string
  icon: number
  score: string
  color: string
  'bg-color': string
}

const props = defineProps({
  results: {
    type: Array as () => Result[],
    required: true,
  },
})

function categoryTextStyle(color: string) {
  return {
    color,
  }
}
const averageScore = computed(() => {
  const total = props.results.reduce((acc, result) => {
    return acc + Number.parseInt(result.score)
  }, 0)
  return Math.round(total / props.results.length)
})
</script>

<template>
  <v-row
    no-gutters
    class="result-container"
  >
    <v-col
      cols="12"
      md="6"
    >
      <v-card
        class="result-card result-card--left fill-height"
        elevation="0"
        color="blue"
        :class="{
          'result-card--mobile': $vuetify.display.smAndDown,
        }"
      >
        <v-card-title
          class="text-center opacity-8"
        >
          <h3>Your Result</h3>
        </v-card-title>
        <v-spacer />
        <div
          class="d-flex flex-column align-center text-center"
        >
          <div
            class="average-score-container my-4"
            :class="{
              'average-score-container--mobile': $vuetify.display.smAndDown,
            }"
          >
            <p
              class="average-score--score"
            >
              {{ averageScore }}
            </p>
            <p class="opacity-6">
              of 100
            </p>
          </div>
        </div>
        <v-spacer />
        <v-card-text
          class="text-center pb-0 flex-grow-0"
        >
          <h1 class="mb-6">
            Great
          </h1>
          <p
            class="opacity-8"
            :class="{
              'text--small': $vuetify.display.smAndDown,
            }"
          >
            You scored higher than 65% of the people who have taken these tests.
          </p>
        </v-card-text>
      </v-card>
    </v-col>
    <v-col
      cols="12"
      md="6"
    >
      <v-card
        class="result-card"
        elevation="0"
        :class="{
          'result-card--mobile': $vuetify.display.smAndDown,
        }"
      >
        <v-card-title>
          <h3>Summary</h3>
        </v-card-title>
        <v-card-text class="mb-0 pb-0">
          <v-card
            v-for="result in results"
            :key="result.category"
            elevation="0"
            rounded="lg"
            class="py-2 px-4 my-4"
            :style="{ 'background-color': `${result['bg-color']}!important` }"
          >
            <div
              class="d-inline-flex my-2 w-100 align-center"
            >
              <div>
                <v-img
                  :src="`/images/${result.icon}`"
                  width="24"
                  height="24"
                />
              </div>
              <p
                class="ml-4"
                :style="categoryTextStyle(result.color)"
              >
                {{ result.category }}
              </p>
              <v-spacer />
              <p>
                <b>{{ result.score }}</b>
                <span class="opacity-6">
                  / 100
                </span>
              </p>
            </div>
          </v-card>
        </v-card-text>
        <v-card-actions class="pb-0">
          <v-btn
            block
            color="#343C59"
            rounded="xl"
            variant="elevated"
            class="continue-btn text-white text-none"
            size="48"
          >
            <p><b>Continue</b></p>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<style scoped lang="scss">
.average-score {
  &--score {
    font-size: 54px;
    font-weight: 700;
    line-height: 1.2;
  }

  &-container {
    border-radius: 50%;
    background-image: linear-gradient(
            hsla(256, 72%, 46%, 1) 0%,
            hsla(241, 72%, 46%, 0) 100%
    );
    width: 185px;
    height: 185px;
    display: flex;
    flex-flow: column nowrap;
    align-content: center;
    justify-content: center;

    &--mobile {
      width: 150px;
      height: 150px;
    }
  }
}
.continue-btn {
  &:hover {
    background-image: linear-gradient(
            hsl(252, 100%, 67%) 0%,
            hsl(241, 81%, 54%) 100%
    );
  }
}
.opacity-8 {
  opacity: 0.8;
}
.opacity-6 {
  opacity: 0.6;
}
.result-container {
  box-shadow: 10px 15px 25px 0px rgba(0,0,0,0.1);
  width: fit-content;
  border-radius: 32px;
}
.result-card {
  border-radius: 32px;
  width: 350px;
  height: 500px;
  padding: 42px 32px;
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;

  &--mobile {
    width: 100%;
    height: fit-content;
    padding-left: 0;
    padding-right: 0;
  }

  &--left {
    background-image: linear-gradient(
            hsl(252, 100%, 67%) 0%,
            hsl(241, 81%, 54%) 100%
    );
  }
}
.text--small {
  font-size: 14px;
  line-height: 1.5;
}
</style>
