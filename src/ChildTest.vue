<template>
  <input :value="state" @input="change" />
</template>

<script lang="ts">
import { watch } from "vue";
import { Aggregation } from "./injection-helper";
export default {
  name: "child-test",
  setup() {
    const state = Aggregation<string>(
      "test",
      ["test", "value", "test", "test", "test", "0"],
      ""
    );
    const test = Aggregation<string>("un-setup-provider", [], "initial");
    setTimeout(() => {
      test.value = "non-provider-injection estanblished";
    }, 1000);
    watch(
      test,
      (res) => {
        console.log(res);
      },
      { immediate: true }
    );
    return {
      state,
      change(e: any) {
        state.value = e.target.value;
      },
    };
  },
};
</script>

<style>
</style>