<template>
  <ValidationProvider
    ref="validator"
    :vid="vid"
    :name="$attrs.name"
    :rules="rules"
  >
    <b-form-group
      id="exampleInputGroup3"
      slot-scope="{ valid, errors }"
      v-bind="$attrs"
    >
      <b-form-select
        id="exampleInput3"
        v-bind="$attrs"
        :state="errors[0] ? false : valid ? true : null"
        v-model="innerValue"
      >
        <slot />
      </b-form-select>
      <b-form-invalid-feedback id="inputLiveFeedback">
        {{ errors[0] }}
      </b-form-invalid-feedback>
    </b-form-group>
  </ValidationProvider>
</template>


<script>
import { ValidationProvider } from "vee-validate";

export default {
  components: {
    ValidationProvider,
  },
  props: {
    vid: {
      type: String,
    },
    rules: {
      type: [Object, String],
      default: "",
    },
    // must be included in props
    value: {
      type: null,
    },
  },
  data: () => ({
    innerValue: "",
  }),
  mounted: () => {
    console.log("select: innerValue=" + this.innerValue);
    console.log("select: value=" + this.value);
  },
  watch: {
    // Handles internal model changes.
    innerValue(newVal) {
      console.log("inner value change: " + newVal);
      console.log("validator", this.$refs.validator);
      this.$emit("input", newVal);
    },
    // Handles external model changes.
    value(newVal) {
      console.log("value change: " + newVal);
      this.innerValue = newVal;
    },
  },
  created() {
    if (this.value) {
      this.innerValue = this.value;
    }
  },
};
</script>
