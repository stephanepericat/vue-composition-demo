<template>
  <button @click="increment">
    Count is: {{ state.count }}, double is: {{ double }}
  </button>
</template>
<script>
import { reactive, computed, watch, onMounted } from "@vue/composition-api";

export default {
  setup() {
    const state = reactive({
      count: 0
    });

    const double = computed(() => state.count * 2);

    function increment() {
      state.count++;
    }

    watch(() => {
      console.log("COUNT >>", state.count);
    });

    watch(() => {
      console.log("DOUBLE >>>", double.value);
    });

    onMounted(() => {
      console.log("COMPONENT MOUNTED >>>", state);
    });

    return {
      double,
      increment,
      state
    };
  }
};
</script>

<style lang="scss"></style>
