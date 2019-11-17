<template>
  <div>count is : {{ state.count }}</div>
</template>
<script>
import { reactive } from "@vue/composition-api";

export default {
  setup() {
    const state = reactive({
      count: 0
    });

    return {
      state
    };
  }
};
</script>

<style lang="scss"></style>
