<template>
  <div class="mt-4 p-4">
    <div class="text-2xl mb-4 text-center">View details of transaction</div>
    <nuxt-link
      :to="`/`"
      class="font-medium text-lime-900 dark:text-blue-500 hover:underline"
      >{{ "<" }} return</nuxt-link
    >
    <Transaction />
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "ViewTransactionsPage",
});
</script>
<style></style>
