<template lang="pug">
  include ../../utils/bem/index.pug
  +b.LABEL.t-radio(:class="classes")
    input(
      v-bind="$attrs" 
      type="radio" 
      :value="value" 
      :checked="isSelected" 
      :disabled="disabled" 
      @change="$emit('input', value)" 
      @focus="focused = true" 
      @blur="focused = false")
    span {{label}}
</template>

<script>
export default {
  name: "TRadio",
  data: () => ({
    focused: false,
  }),
  inheritAttrs: false,
  model: {
    prop: "model",
  },
  props: {
    model: {
      type: [String, Number, Boolean, Object],
      required: true,
    },
    value: {
      type: [String, Number, Boolean, Object],
      required: true,
    },
    label: String,
    disabled: Boolean,
  },
  computed: {
    classes() {
      return {
        checked: this.isSelected,
        disabled: this.disabled,
        focused: this.focused,
      };
    },
    isValueObject() {
      return this.value !== null && typeof this.value === "object";
    },
    isSelected() {
      if (this.isValueObject) {
        return this.isObjectEqual(this.model, this.value);
      }

      return this.model === this.value;
    },
  },
  methods: {
    isObjectEqual(a, b) {
      return JSON.stringify(a) === JSON.stringify(b);
    },
  },
};
</script>

<style lang="scss"></style>
