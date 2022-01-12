<script>
export default /*#__PURE__*/ {
  name: "VueMzcCounter",
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

<style>
:root {
  --vue-mzc-counter-width: 120px;
  --vue-mzc-counter-height: 32px;
  --vue-mzc-counter-text-size: 14px;
  --vue-mzc-counter-unit-size: 12px;
  --vue-mzc-counter-text-color: #242424;
  --vue-mzc-counter-border-color: #cccccc;
  --vue-mzc-counter-disabled-color: #aaaaaa;
  --vue-mzc-counter-background-color: #ffffff;
  --vue-mzc-counter-primary-color: #306EC4;
  --vue-mzc-counter-glow-color: rgba(48, 110, 196, 0.15);
  --vue-mzc-counter-border-width: 1px;
  --vue-mzc-counter-border-radius: 4px;
}
.vue-mzc-counter {
  display: flex;
  width: 120px;
  width: var(--vue-mzc-counter-width);
}
.vue-mzc-counter__input,
.vue-mzc-counter__button {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  height: 32px;
  height: var(--vue-mzc-counter-height);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: inherit;
  font-size: 14px;
  font-size: var(--vue-mzc-counter-text-size);
  color: #242424;
  color: var(--vue-mzc-counter-text-color);
  transition: color 0.25s ease-in-out; 
}
.vue-mzc-counter__button:disabled {
  color: #aaaaaa;
  color: var(--vue-mzc-counter-disabled-color);
}
.vue-mzc-counter__input {
  flex: 1;
  background-color: #ffffff;
  background-color: var(--vue-mzc-counter-background-color);
  border-width: 1px;
  border-width: var(--vue-mzc-counter-border-width);
  border-style: solid;
  border-color: #cccccc;
  border-color: var(--vue-mzc-counter-border-color);
  border-radius: 4px;
  border-radius: var(--vue-mzc-counter-border-radius);
  text-align: center;
  transition: border-color 0.25s ease-in-out, box-shadow 0.25s ease-in-out;
}
.vue-mzc-counter__count,
input.vue-mzc-counter__input {
  font-weight: 700;
}
input.vue-mzc-counter__input:focus {
  outline: none;
  border-color: #306EC4;
  border-color: var(--vue-mzc-counter-primary-color);
  box-shadow: 0 0 8px 0 rgba(48, 110, 196, 0.15);
  box-shadow: 0 0 8px 0 var(--vue-mzc-counter-glow-color);
}
.vue-mzc-counter__input::-webkit-outer-spin-button,
.vue-mzc-counter__input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
.vue-mzc-counter__button {
  cursor: pointer;
  width: 32px;
  font-weight: 700;
  background-color: transparent;
  border: none;
}
.vue-mzc-counter__unit {
  padding-left: 1px;
  font-size: 12px;
  font-size: var(--vue-mzc-counter-unit-size);
}
</style>