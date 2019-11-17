<template>
  <button @click="increment" class="btn">
    Count is: {{ state.count }}, double is: {{ double }}
  </button>
</template>
<script>
import { reactive, computed, watch, onMounted } from "@vue/composition-api";

export default {
  setup() {
    /**
     * Initial State
     */
    const state = reactive({
      count: 0
    });

    /**
     * Computed Properties
     */
    const double = computed(() => state.count * 2);

    /**
     * Methods
     */
    function increment() {
      state.count++;
    }

    /**
     * Watchers
     */
    watch(() => {
      console.log("COUNT >>", state.count);
    });

    watch(() => {
      console.log("DOUBLE >>>", double.value);
    });

    /**
     * Lifecycle Hooks
     */
    onMounted(() => {
      console.log("COMPONENT MOUNTED >>>", state);
    });

    /**
     * return what the template needs...
     */
    return {
      double,
      increment,
      state
    };
  }
};
</script>

<style lang="scss">
.btn {
  border: 1px solid #ccc;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 4px;
  cursor: pointer;
  background: #eee;

  &:hover {
    background: #ddd;
  }
}
</style>
