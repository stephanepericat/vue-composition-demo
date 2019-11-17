<script>
import {
  computed,
  createComponent,
  onMounted,
  reactive,
  watch
} from "@vue/composition-api";

export default createComponent({
  /**
   * Props
   */
  props: {
    foo: String
  },

  /**
   * Setup method
   * @param props {Object} the component's props
   * @param context {Object} the current context
   */
  setup(props) {
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
    const FOO = computed(() => props.foo.toUpperCase());

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
      FOO,
      increment,
      state
    };
  },

  /**
   * @method render
   * @param createElement {Function}
   * Supports both "createElement" and JSX templates
   */
  render() {
    const { double, foo, FOO, increment, state } = this;

    // JSX
    return (
      <div>
        <button onClick={increment} className="btn">
          Count is: {state.count}, double is: {double}
        </button>
        <p>
          foo is: {foo}, upper-cased: {FOO}
        </p>
      </div>
    );
  }
});
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
