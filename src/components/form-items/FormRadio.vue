<template>
  <fieldset>
    <legend>{{ label }}</legend>

    <div
        v-for="option in options"
        :key="option.value"
    >
      <input required type="radio" name="radio" :value="option.value" :checked="option.selected" @change="updateRadio"/>
      <label :for="option.value">{{ option.text }}</label>
    </div>
  </fieldset>
</template>

<script>
export default {
  name: "FormRadio",

  props: {
    label: {
      type: String,
      default: ''
    },

    options: {
      type: Object,
      required: true
    },
  },
  methods: {
    updateRadio(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  },
  mounted() {
    const selectedOption = this.options.find(option => option.selected);
    if (selectedOption) {
      this.$emit('update:modelValue', selectedOption.value);
    }
  },
}
</script>

<style scoped lang="scss">
fieldset {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
  border: 1px solid #b578c0;
  border-radius: 10px;
  div {
    display: flex;
    align-items: center;
    gap: 8px;
    input {
      height: 15px;
      width: 15px;
      cursor: pointer;
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      border: 1px solid #b578c0;
      border-radius: 10px;
      &:checked {
        background-color: rgb(118, 54, 223);
    }
    }
    label {
      font-size: 16px;
      line-height: 100%;
    }
  }
}
</style>
