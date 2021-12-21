<script>
export default /*#__PURE__*/ {
  name: "VueMzcCounter", // vue component name
  data() {
    return {
      count: this.value <= this.max ? this.value : this.max,
      editable: false,
    };
  },
  props: {
    value: {
      type: Number,
      default: 1,
    },
    max: {
      type: Number,
      default: 1,
    },
    unit: {
      type: String,
      default: "",
    },
  },
  methods: {
    increment() {
      if (this.count < this.max) {
        this.count = parseInt(this.count) + 1;
        this.$emit("change", this.count);
      }
    },
    decrement() {
      if (this.count > 1) {
        this.count = parseInt(this.count) - 1;
        this.$emit("change", this.count);
      }
    },
    edit() {
      this.editable = true;
      this.$nextTick(() => {
        this.$refs.input.focus();
      });
    },
    change(count) {
      if (parseInt(count) > this.max) {
        this.count = this.max;
        this.$emit("change", this.count);
      } else {
        this.$emit("change", parseInt(count));
      }
    },
  },
};
</script>

<template>
  <div class="vue-mzc-counter">
    <button
      class="vue-mzc-counter__button"
      :disabled="count <= 1"
      @click="decrement"
    >
      −
    </button>
    <input
      v-if="editable"
      v-model="count"
      class="vue-mzc-counter__input"
      ref="input"
      type="number"
      min="1"
      :max="max"
      @blur="editable = false"
      @keyup.enter="(e) => e.target.blur()"
      @change="(e) => change(e.target.value)"
    />
    <span
      v-else
      class="vue-mzc-counter__input"
      tabindex="0"
      @click="edit"
      @keyup.enter="edit"
    >
      <span class="vue-mzc-counter__value">
        <span class="vue-mzc-counter__count">{{ count }}</span>
        <span class="vue-mzc-counter__unit">{{ unit }}</span>
      </span>
    </span>
    <button
      class="vue-mzc-counter__button"
      :disabled="count >= max"
      @click="increment"
    >
      +
    </button>
  </div>
</template>
