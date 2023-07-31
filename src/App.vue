<script setup lang="ts">
import ResultSummary from '~/components/ResultSummary.vue'
import data from '~/assets/data.json'
</script>

<template>
  <v-app>
    <v-main>
      <v-container
        class="fill-height d-flex flex-column"
      >
        <v-spacer />
        <div>
          <ResultSummary :results="data as any" />
        </div>
        <v-spacer />
        <div class="attribution text-center w-100">
          Challenge by <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>.
          Coded by <a href="https://github.com/Antoine340">@Antoine340</a>.
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>
