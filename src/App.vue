<script>
import {
  computed,
  createComponent,
  onMounted,
  reactive,
  ref,
  set,
  toRefs,
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
   * @method setup
   * @param props {Object} the component's props
   * @param context {Object} the current context
   * Set up your state, refs, computed props, methods, watchers, lifecycle hooks...
   * Whatever you export here will be available in render()
   */
  setup(props) {
    /**
     * Initial State
     */
    const state = reactive({
      count: 0,
      username: "John Doe"
    });

    /**
     * Template Refs
     */
    const nameInputRef = ref(null);

    /**
     * Computed Properties
     */
    const double = computed(() => state.count * 2);
    const FOO = computed(() => props.foo.toUpperCase());

    /**
     * Methods
     */
    function increment() {
      set(state, "count", state.count + 1);
    }

    function updateUsername(e) {
      set(state, "username", e.target.value);
    }

    /**
     * Watchers
     */
    watch(() => {
      console.log(`COUNT >>> ${state.count}, DOUBLE >>> ${double.value}`);
    });

    watch(() => {
      console.log("USERNAME >>>", state.username);
    });

    /**
     * Lifecycle Hooks
     */
    onMounted(() => {
      console.log("COMPONENT MOUNTED..");
      console.log("nameInputRef >>>", nameInputRef.value);
    });

    /**
     * return what the template needs...
     */
    return {
      double,
      FOO,
      increment,
      nameInputRef,
      updateUsername,
      // You can use `toRefs` to make the state spreadable
      ...toRefs(state)
    };
  },

  /**
   * @method render
   * @param createElement {Function}
   * Supports both "createElement" and JSX templates
   */
  render() {
    const {
      count,
      double,
      foo,
      FOO,
      increment,
      updateUsername,
      username
    } = this;

    // JSX
    return (
      <div>
        <button onClick={increment} className="btn">
          Count is: {count}, double is: {double}
        </button>
        <p>
          foo is: {foo}, upper-cased: {FOO}
        </p>
        <input
          type="text"
          value={username}
          onInput={updateUsername}
          ref="nameInputRef"
        />
        {username && <p>Username: {username}</p>}
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
